---
title: material_test
date: 2020-05-07
---
Example Python program material_test.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import textwrap
* import sys
* from PyQt5.QtQuick import (
* from PyQt5.QtQml import (
* from PyQt5.QtCore import pyqtProperty, pyqtSignal, QUrl, QTimer
* from PyQt5.QtWidgets import QApplication
* import sip

## Classes

* class MyMaterialShader(QSGMaterialShader):
* class MyMaterial(QSGMaterial):
* class CustomShaderItem(QQuickItem):
* # Python Exception <class 'RuntimeError'> Type does not have a target.:
* # Python Exception <class 'RuntimeError'> Type does not have a target.:

## Methods

* def __init__(self):
* def updateState(self, state, material, old_material):
* def attributeNames(self):
* def initialize(self):
* def vertexShader(self):
* def fragmentShader(self):
* def __del__(self):
* def __init__(self):
* def compare(self, other_material):
* def createShader(self):
* def type(self):
* def __init__(self):
* def updatePaintNode(self, root_node, node_data):
* def main():

## Code

Example Python PyQt program :

    # PyQt 5.4.2 bug example: QSGMaterial::createShader() result object is destroyed
    # before use + application hangs at exit
    
    import textwrap
    import sys
    
    from PyQt5.QtQuick import (
        QQuickItem, QSGMaterial,
        QSGMaterialShader, QSGMaterialType,
        QSGGeometry, QSGGeometryNode, QSGNode, QQuickView
        )
    from PyQt5.QtQml import (
        qmlRegisterType, QQmlEngine, QQmlComponent, QQmlImageProviderBase,
        QQmlProperty)
    from PyQt5.QtCore import pyqtProperty, pyqtSignal, QUrl, QTimer
    from PyQt5.QtWidgets import QApplication
    
    
    class MyMaterialShader(QSGMaterialShader):
        def __init__(self):
            super().__init__()
    
            self._matrix_uniform_id = None
    
            print("MyMaterialShader() created")
    
        def updateState(self, state, material, old_material):
            if state.isMatrixDirty():
                self.program().setUniformValue(
                    self._matrix_uniform_id, state.combinedMatrix())
    
            if not isinstance(material, MyMaterial):
                return
    
        def attributeNames(self):
            return ["qt_VertexPosition", "qt_VertexTexCoord"]
    
        def initialize(self):
            self._matrix_uniform_id = self.program().uniformLocation("qt_Matrix")
    
        def vertexShader(self):
            return textwrap.dedent("""\
                uniform highp mat4 qt_Matrix;
    
                attribute highp vec4 qt_VertexPosition;
                attribute highp vec2 qt_VertexTexCoord;
    
                varying highp vec2 qt_TexCoord;
    
                void main()
                {
                    qt_TexCoord = qt_VertexTexCoord;
                    gl_Position = qt_Matrix * qt_VertexPosition;
                }
                """)
    
        def fragmentShader(self):
            return textwrap.dedent("""\
                varying highp vec2 qt_TexCoord;
    
                void main()
                {
                    gl_FragColor = vec4(qt_TexCoord.x, qt_TexCoord.y, 1, 1);
                }
                """)
    
        def __del__(self):
            print("MyMaterialShader() destroyed")
    
    
    class MyMaterial(QSGMaterial):
        _type = QSGMaterialType()
    
        def __init__(self):
            super().__init__()
    
        def compare(self, other_material):
            if self is other_material:
                return 0
            else:
                return -1 if id(self) < id(other_material) else 1
    
        def createShader(self):
            shader = MyMaterialShader()
    
            # Problem #1: created in Python QSGMaterialShader object is being
            # destroyed when not referenced by Python.
            # QSGMaterialShader's are cached inside Qt and rarely destroyed,
            # so Qt fails with segfault when tries to use destroyed object.
    
            # Workaround: store Python QSGMaterialShader objects indefinitely.
            self._shader = shader  # uncomment this for workaround
    
            return shader
    
        def type(self):
            return self._type
    
    
    class CustomShaderItem(QQuickItem):
        def __init__(self):
            super().__init__()
    
            self.setFlag(QQuickItem.ItemHasContents, True)
    
        def updatePaintNode(self, root_node, node_data):
            print("Root node:", root_node)
            if root_node is None:
                root_node = QSGGeometryNode()
    
                material = MyMaterial()
                root_node.setMaterial(material)
                root_node.setFlag(QSGNode.OwnsMaterial)
    
                x = 0
                y = 0
                width = 100
                height = 100
    
                geometry = QSGGeometry(
                    QSGGeometry.defaultAttributes_TexturedPoint2D(),
                    5)
                geometry.setDrawingMode(QSGGeometry.GL_TRIANGLE_STRIP)
                root_node.setGeometry(geometry)
                root_node.setFlag(QSGNode.OwnsGeometry)
    
                vertices = geometry.vertexDataAsTexturedPoint2D()
                vertices[0].set(x, y, 0, 0)
                vertices[1].set(x + width, y, 1, 0)
                vertices[2].set(x + width, y + height, 1, 1)
                vertices[3].set(x, y + height, 0, 1)
                vertices[4].set(x, y, 0, 0)
    
                root_node.markDirty(QSGNode.DirtyGeometry)
                root_node.markDirty(QSGNode.DirtyMaterial)
    
                # According to documentation, lifetime of QSGNode is managed by Qt,
                # so we cannot safely store it in Python.
                # Transfer ownership to C++ to workaround this issue.
                import sip
                sip.transferto(root_node, root_node)
    
            return root_node
    
    
    def main():
        app = QApplication(sys.argv)
    
        qml_engine = QQmlEngine()
    
        view = QQuickView(qml_engine, None)
    
        scene_uri = QUrl.fromLocalFile("MaterialTest.qml")
        view.setSource(scene_uri)
        assert not view.errors()
    
        shader_item = CustomShaderItem()
        shader_item.setProperty("parent", view.rootObject())
    
        view.show()
    
        exit_code = app.exec_()
    
        #print("Destroying QQuickView")
        #del view
        #print("QQuickView destroyed")
        # Problem #2: destroying QQuickView that used Python-created QSGGeometryNode
        # leads to deadlock.
        #
        # As I see, when QQuickView is being destroyed it waits until render thread
        # clean ups all resources, which causes QSGGeometryNode to be destroyed,
        # which asks to lock GIL, which is still locked by main thread.
        #
        # Here is stack traces at the moment of deadlock:
        #
        #     (gdb) info threads
        #       Id   Target Id         Frame
        #       4    Thread 0x7f705ca83700 (LWP 23802) "QXcbEventReader" 0x00007f706b51c12d in poll () at ../sysdeps/unix/syscall-template.S:81
        #       3    Thread 0x7f7057df9700 (LWP 23803) "QQmlThread" 0x00007f706b51c12d in poll () at ../sysdeps/unix/syscall-template.S:81
        #       2    Thread 0x7f7055aa7700 (LWP 23804) "QSGRenderThread" pthread_cond_timedwait@@GLIBC_2.3.2 () at ../nptl/sysdeps/unix/sysv/linux/x86_64/pthread_cond_timedwait.S:238
        #     * 1    Thread 0x7f706bf21780 (LWP 23801) "python" pthread_cond_wait@@GLIBC_2.3.2 () at ../nptl/sysdeps/unix/sysv/linux/x86_64/pthread_cond_wait.S:185
        #     (gdb) bt
        #     #0  pthread_cond_wait@@GLIBC_2.3.2 () at ../nptl/sysdeps/unix/sysv/linux/x86_64/pthread_cond_wait.S:185
        #     #1  0x00007f706505e482 in QWaitConditionPrivate::wait (this=0x2cffb00, time=18446744073709551615) at thread/qwaitcondition_unix.cpp:136
        #     #2  0x00007f706505e255 in QWaitCondition::wait (this=0x2cff538, mutex=0x2cff530, time=18446744073709551615) at thread/qwaitcondition_unix.cpp:208
        #     #3  0x00007f70664b4527 in QSGThreadedRenderLoop::releaseResources (this=0x2a09600, w=0x27dcb80, inDestructor=true) at scenegraph/qsgthreadedrenderloop.cpp:1059
        #     #4  0x00007f70664b2ed8 in QSGThreadedRenderLoop::windowDestroyed (this=0x2a09600, window=0x2768670) at scenegraph/qsgthreadedrenderloop.cpp:825
        #     #5  0x00007f70664ad512 in QSGRenderLoop::cleanup () at scenegraph/qsgrenderloop.cpp:94
        #     #6  0x00007f70652d2c9e in qt_call_post_routines () at kernel/qcoreapplication.cpp:294
        #     #7  0x00007f705fdc6734 in QApplication::~QApplication (this=0x26c6ed0, __in_chrg=<optimized out>) at kernel/qapplication.cpp:808
        #     #8  0x00007f70607e5758 in sipQApplication::~sipQApplication (this=0x26c6ed0, __in_chrg=<optimized out>) at sipQtWidgetspart0.cpp:301912
        #     #9  0x00007f70607e5788 in sipQApplication::~sipQApplication (this=0x26c6ed0, __in_chrg=<optimized out>) at sipQtWidgetspart0.cpp:301915
        #     #10 0x00007f70607e8f21 in release_QApplication (sipCppV=0x26c6ed0) at sipQtWidgetspart0.cpp:303524
        #     #11 0x00007f70607e8fba in dealloc_QApplication (sipSelf=0x7f705fc42168) at sipQtWidgetspart0.cpp:303538
        #     #12 0x00007f7061cae346 in ?? () from /home/bob/work/proplan/env/lib/python3.4/site-packages/sip.so
        #     #13 0x00007f7061caf5e9 in ?? () from /home/bob/work/proplan/env/lib/python3.4/site-packages/sip.so
        #     #14 0x0000000000598732 in subtype_dealloc.lto_priv () at ../Objects/typeobject.c:1201
        #     #15 0x00000000004c88c7 in frame_dealloc.lto_priv () at ../Objects/frameobject.c:429
        #     #16 0x0000000000503dfb in fast_function (nk=<optimized out>, na=<optimized out>, n=0, pp_stack=0x7ffd401cf350, func=<optimized out>) at ../Python/ceval.c:4336
        #     #17 call_function (oparg=<optimized out>, pp_stack=0x7ffd401cf350) at ../Python/ceval.c:4262
        #     #18 PyEval_EvalFrameEx () at ../Python/ceval.c:2838
        #     #19 0x00000000005a9cb5 in PyEval_EvalCodeEx () at ../Python/ceval.c:3588
        #     Python Exception <class 'RuntimeError'> Type does not have a target.:
        #     Python Exception <class 'RuntimeError'> Type does not have a target.:
        #     #20 0x00000000005e7105 in PyEval_EvalCode (locals=, globals=, co=<code at remote 0x7f706bdf5420>) at ../Python/ceval.c:775
        #     #21 run_mod () at ../Python/pythonrun.c:2180
        #     #22 0x00000000005e71c9 in PyRun_FileExFlags () at ../Python/pythonrun.c:2133
        #     #23 0x00000000005e79aa in PyRun_SimpleFileExFlags () at ../Python/pythonrun.c:1606
        #     #24 0x00000000005fb69d in run_file (p_cf=<optimized out>, filename=<optimized out>, fp=<optimized out>) at ../Modules/main.c:319
        #     #25 Py_Main () at ../Modules/main.c:751
        #     #26 0x00000000004c2e7f in main () at ../Modules/python.c:69
        #     #27 0x00007f706b450ec5 in __libc_start_main (main=0x4c2da0 <main>, argc=2, argv=0x7ffd401cf7c8, init=<optimized out>, fini=<optimized out>, rtld_fini=<optimized out>, stack_end=0x7ffd401cf7b8)
        #         at libc-start.c:287
        #     #28 0x00000000005b8db9 in _start ()
        #     (gdb) thread 2
        #     [Switching to thread 2 (Thread 0x7f7055aa7700 (LWP 23804))]
        #     #0  pthread_cond_timedwait@@GLIBC_2.3.2 () at ../nptl/sysdeps/unix/sysv/linux/x86_64/pthread_cond_timedwait.S:238
        #     238     ../nptl/sysdeps/unix/sysv/linux/x86_64/pthread_cond_timedwait.S: No such file or directory.
        #     (gdb) bt
        #     #0  pthread_cond_timedwait@@GLIBC_2.3.2 () at ../nptl/sysdeps/unix/sysv/linux/x86_64/pthread_cond_timedwait.S:238
        #     #1  0x00000000004ff96c in PyCOND_TIMEDWAIT (cond=<optimized out>, mut=<optimized out>, us=5000) at ../Python/condvar.h:103
        #     #2  take_gil.lto_priv () at ../Python/ceval_gil.h:224
        #     #3  0x00000000004ffb43 in PyEval_RestoreThread () at ../Python/ceval.c:448
        #     #4  0x00000000005e7c67 in PyGILState_Ensure () at ../Python/pystate.c:793
        #     #5  0x00007f7061cb6307 in ?? () from /home/bob/work/proplan/env/lib/python3.4/site-packages/sip.so
        #     #6  0x00007f7066888341 in sipQSGGeometryNode::~sipQSGGeometryNode (this=0x7f70480e6580, __in_chrg=<optimized out>) at sipQtQuickpart0.cpp:7733
        #     #7  0x00007f706688837c in sipQSGGeometryNode::~sipQSGGeometryNode (this=0x7f70480e6580, __in_chrg=<optimized out>) at sipQtQuickpart0.cpp:7734
        #     #8  0x00007f706646a178 in QSGNode::destroy (this=0x7f70480e6210) at scenegraph/coreapi/qsgnode.cpp:389
        #     #9  0x00007f706646a01d in QSGNode::~QSGNode (this=0x7f70480e6210, __in_chrg=<optimized out>) at scenegraph/coreapi/qsgnode.cpp:320
        #     #10 0x00007f706646a05c in QSGNode::~QSGNode (this=0x7f70480e6210, __in_chrg=<optimized out>) at scenegraph/coreapi/qsgnode.cpp:321
        #     #11 0x00007f706646a178 in QSGNode::destroy (this=0x7f70480e6080) at scenegraph/coreapi/qsgnode.cpp:389
        #     #12 0x00007f706646a01d in QSGNode::~QSGNode (this=0x7f70480e6080, __in_chrg=<optimized out>) at scenegraph/coreapi/qsgnode.cpp:320
        #     #13 0x00007f706646b49e in QSGTransformNode::~QSGTransformNode (this=0x7f70480e6080, __in_chrg=<optimized out>) at scenegraph/coreapi/qsgnode.cpp:1156
        #     #14 0x00007f706646b4ce in QSGTransformNode::~QSGTransformNode (this=0x7f70480e6080, __in_chrg=<optimized out>) at scenegraph/coreapi/qsgnode.cpp:1158
        #     #15 0x00007f70664efcb7 in QQuickWindowPrivate::cleanupNodesOnShutdown (item=0x273d390) at items/qquickwindow.cpp:2588
        #     #16 0x00007f70664effc4 in QQuickWindowPrivate::cleanupNodesOnShutdown (item=0x2d31f90) at items/qquickwindow.cpp:2616
        #     #17 0x00007f70664effc4 in QQuickWindowPrivate::cleanupNodesOnShutdown (item=0x2a052d0) at items/qquickwindow.cpp:2616
        #     #18 0x00007f70664f002b in QQuickWindowPrivate::cleanupNodesOnShutdown (this=0x2a057b0) at items/qquickwindow.cpp:2624
        #     #19 0x00007f70664b0df5 in QSGRenderThread::invalidateOpenGL (this=0x2cff4f0, window=0x2768670, inDestructor=true, fallback=0x2cff590) at scenegraph/qsgthreadedrenderloop.cpp:465
        #     #20 0x00007f70664b0520 in QSGRenderThread::event (this=0x2cff4f0, e=0x2cfd3f0) at scenegraph/qsgthreadedrenderloop.cpp:390
        #     #21 0x00007f70664b2078 in QSGRenderThread::processEventsAndWaitForMore (this=0x2cff4f0) at scenegraph/qsgthreadedrenderloop.cpp:644
        #     #22 0x00007f70664b23f3 in QSGRenderThread::run (this=0x2cff4f0) at scenegraph/qsgthreadedrenderloop.cpp:672
        #     #23 0x00007f706505cd9b in QThreadPrivate::start (arg=0x2cff4f0) at thread/qthread_unix.cpp:337
        #     #24 0x00007f706b7fc182 in start_thread (arg=0x7f7055aa7700) at pthread_create.c:312
        #     #25 0x00007f706b52947d in clone () at ../sysdeps/unix/sysv/linux/x86_64/clone.S:111
        #     (gdb) thread 3
        #     [Switching to thread 3 (Thread 0x7f7057df9700 (LWP 23803))]
        #     #0  0x00007f706b51c12d in poll () at ../sysdeps/unix/syscall-template.S:81
        #     81      ../sysdeps/unix/syscall-template.S: No such file or directory.
        #     (gdb) bt
        #     #0  0x00007f706b51c12d in poll () at ../sysdeps/unix/syscall-template.S:81
        #     #1  0x00007f7063bc0fe4 in g_main_context_poll (priority=2147483647, n_fds=1, fds=0x7f70500013e0, timeout=-1, context=0x7f70500009b0) at /build/buildd/glib2.0-2.40.2/./glib/gmain.c:4028
        #     #2  g_main_context_iterate (context=context@entry=0x7f70500009b0, block=block@entry=1, dispatch=dispatch@entry=1, self=<optimized out>) at /build/buildd/glib2.0-2.40.2/./glib/gmain.c:3729
        #     #3  0x00007f7063bc10ec in g_main_context_iteration (context=0x7f70500009b0, may_block=1) at /build/buildd/glib2.0-2.40.2/./glib/gmain.c:3795
        #     #4  0x00007f706534d149 in QEventDispatcherGlib::processEvents (this=0x7f70500008e0, flags=...) at kernel/qeventdispatcher_glib.cpp:418
        #     #5  0x00007f70652d0f1e in QEventLoop::processEvents (this=0x7f7057df8e10, flags=...) at kernel/qeventloop.cpp:128
        #     #6  0x00007f70652d11df in QEventLoop::exec (this=0x7f7057df8e10, flags=...) at kernel/qeventloop.cpp:204
        #     #7  0x00007f70650558e0 in QThread::exec (this=0x2732370) at thread/qthread.cpp:503
        #     #8  0x00007f706598c5c5 in QQmlThreadPrivate::run (this=0x2732370) at qml/ftw/qqmlthread.cpp:141
        #     #9  0x00007f706505cd9b in QThreadPrivate::start (arg=0x2732370) at thread/qthread_unix.cpp:337
        #     #10 0x00007f706b7fc182 in start_thread (arg=0x7f7057df9700) at pthread_create.c:312
        #     #11 0x00007f706b52947d in clone () at ../sysdeps/unix/sysv/linux/x86_64/clone.S:111
        #     (gdb) thread 4
        #     [Switching to thread 4 (Thread 0x7f705ca83700 (LWP 23802))]
        #     #0  0x00007f706b51c12d in poll () at ../sysdeps/unix/syscall-template.S:81
        #     81      in ../sysdeps/unix/syscall-template.S
        #     (gdb) bt
        #     #0  0x00007f706b51c12d in poll () at ../sysdeps/unix/syscall-template.S:81
        #     #1  0x00007f7067770b72 in poll (__timeout=-1, __nfds=1, __fds=0x7f705ca82d00) at /usr/include/x86_64-linux-gnu/bits/poll2.h:46
        #     #2  _xcb_conn_wait (c=c@entry=0x28a2c60, cond=cond@entry=0x28a2ca0, vector=vector@entry=0x0, count=count@entry=0x0) at ../../src/xcb_conn.c:447
        #     #3  0x00007f706777264f in xcb_wait_for_event (c=0x28a2c60) at ../../src/xcb_in.c:622
        #     #4  0x00007f705fb3df81 in QXcbEventReader::run (this=0x28b0b90) at qxcbconnection.cpp:1105
        #     #5  0x00007f706505cd9b in QThreadPrivate::start (arg=0x28b0b90) at thread/qthread_unix.cpp:337
        #     #6  0x00007f706b7fc182 in start_thread (arg=0x7f705ca83700) at pthread_create.c:312
        #     #7  0x00007f706b52947d in clone () at ../sysdeps/unix/sysv/linux/x86_64/clone.S:111
        #
        # (This issue is not reproduces in Windows, since Qt 5.4 still uses single
        # threaded rendering there.)
    
        return exit_code
    
    
    if __name__ == "__main__":
        exit_code = main()
        sys.exit(exit_code)
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
