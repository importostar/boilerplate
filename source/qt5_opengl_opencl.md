---
title: qt5_opengl_opencl
date: 2020-05-07
---
Example Python program qt5_opengl_opencl.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import ctypes
* import signal
* import numpy
* import pyopencl as cl
* from pyopencl.tools import get_gl_sharing_context_properties
* from OpenGL import GL, GLU
* from PyQt5 import QtCore, QtGui, QtWidgets

## Classes

* class Window(QtWidgets.QWidget):
* class Widget(QtWidgets.QOpenGLWidget):

## Methods

* def compile_shader(shader):
* def build_draw_program(vertex_shader, fragment_shader):
* def build_vbo(vao, data):
* def attach_vertices(vao, program, name, data, dim=2):
* def __init__(self):
* def __init__(self):
* def log_debug_message(self, msg):
* def initializeGL(self):
* def setupCL(self):
* def initializeCL(self):
* def execute_cl_load(self, i=0):
* def execute_cl_invert(self, src=0):
* def paintGL(self):
* def tick(self):
* def resizeGL(self, w, h):
* def main():

## Code

Example Python PyQt program :

    # Minimal PyQt5 + PyOpenGL + PyOpenCl interop over double buffered shared 2d texture
    
    import sys
    import ctypes
    import signal
    
    import numpy
    import pyopencl as cl
    from pyopencl.tools import get_gl_sharing_context_properties
    from OpenGL import GL, GLU
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    position_data = (ctypes.c_float*12)(
        -1, -1, 1, -1, -1, 1, 1, -1, 1, 1, -1, 1)
    
    vertex_shader = (GL.GL_VERTEX_SHADER, '''
        #version 150
    
        in vec2 position;
        out vec2 coord;
    
        void main() {
            gl_Position = vec4(position, 0.0, 1.0);
            coord = vec2(position.x/2.0+0.5, position.y/2.0+0.5);
        }
    ''')
    
    fragment_shader = (GL.GL_FRAGMENT_SHADER, '''
        #version 150
    
        in vec2 coord;
        out vec4 color;
        uniform usampler2D tex;
    
        void main() {
            color = vec4(texture(tex, coord))/255.0;
        }
    ''')
    
    kernel = '''
        const sampler_t sampler = CLK_NORMALIZED_COORDS_FALSE
                                | CLK_ADDRESS_CLAMP_TO_EDGE
                                | CLK_FILTER_NEAREST;
        __kernel void load(
            read_only image2d_t input,
            read_write image2d_t output) {
            int2 pos = (int2)(get_global_id(0), get_global_id(1));
            uint4 cell = read_imageui(input, sampler, pos);
            write_imageui(output, pos, cell);
        }
    
        __kernel void invert(read_only image2d_t src, write_only image2d_t dst) {
            int2 pos = (int2)(get_global_id(0), get_global_id(1));
            uint4 cell = read_imageui(src, sampler, pos);
            cell = 255 - cell;
            write_imageui(dst, pos, cell);
        }
    '''
    
    
    def compile_shader(shader):
        shader_type, shader_source = shader
        shader_id = GL.glCreateShader(shader_type)
        GL.glShaderSource(shader_id, shader_source)
        GL.glCompileShader(shader_id)
        compile_status = GL.glGetShaderiv(shader_id, GL.GL_COMPILE_STATUS)
        assert compile_status
        return shader_id
    
    
    def build_draw_program(vertex_shader, fragment_shader):
        program = GL.glCreateProgram()
        vertex = compile_shader(vertex_shader)
        fragment = compile_shader(fragment_shader)
        GL.glAttachShader(program, vertex)
        GL.glAttachShader(program, fragment)
        GL.glLinkProgram(program)
        link_status = GL.glGetProgramiv(program, GL.GL_LINK_STATUS)
        assert link_status
        return program
    
    
    def build_vbo(vao, data):
        vbo = GL.glGenBuffers(1)
        GL.glBindBuffer(GL.GL_ARRAY_BUFFER, vbo)
        GL.glBufferData(GL.GL_ARRAY_BUFFER, data, GL.GL_DYNAMIC_DRAW)
        return vbo
    
    
    def attach_vertices(vao, program, name, data, dim=2):
        vbo = build_vbo(vao, data)
        attr = GL.glGetAttribLocation(program, name)
        GL.glEnableVertexAttribArray(attr)
        GL.glVertexAttribPointer(attr, dim, GL.GL_FLOAT, GL.GL_FALSE, 0, None)
        return vbo
    
    
    class Window(QtWidgets.QWidget):
        def __init__(self):
            super().__init__()
            self.widget = Widget()
            layout = QtWidgets.QHBoxLayout()
            layout.addWidget(self.widget)
            self.setLayout(layout)
    
    
    class Widget(QtWidgets.QOpenGLWidget):
        def __init__(self):
            super().__init__()
            surface_format = QtGui.QSurfaceFormat()
            surface_format.setMajorVersion(3)
            surface_format.setMajorVersion(2)
            surface_format.setProfile(QtGui.QSurfaceFormat.CoreProfile)
            surface_format.setOption(QtGui.QSurfaceFormat.DebugContext)
            self.setFormat(surface_format)
            self.data = numpy.random.uniform(0, 0x100, (40, 40, 4)).astype('uint8')
            self.timer = QtCore.QTimer()
            self.timer.start(1000)
            self.timer.timeout.connect(self.tick)
            self.cur_buf = 0
    
        def log_debug_message(self, msg):
            print(msg.message())
    
        def initializeGL(self):
            self.makeCurrent()
            self.ctx = self.context()
            self.logger = QtGui.QOpenGLDebugLogger(self)
            self.logger.initialize()
            self.logger.messageLogged.connect(self.log_debug_message)
            self.logger.startLogging()
            draw_program = build_draw_program(vertex_shader, fragment_shader)
            GL.glUseProgram(draw_program)
            self.vao = GL.glGenVertexArrays(1)
            GL.glBindVertexArray(self.vao)
            self.pos_vbo = attach_vertices(self.vao, draw_program,
                                           'position', position_data)
            self.setupCL()
            self.initializeCL()
    
        def setupCL(self):
            platforms = cl.get_platforms()
            clprops = [(cl.context_properties.PLATFORM, platforms[0])]
            ctx = cl.Context(properties=clprops +
                             get_gl_sharing_context_properties())
            queue = cl.CommandQueue(ctx)
            self.clctx = ctx
            self.clqueue = queue
    
        def initializeCL(self):
            W, H, D = self.data.shape
            ctx, queue = self.clctx, self.clqueue
            self.cltex = cl.image_from_array(ctx, self.data, 4)
            self.tex = []
            self.glcltex = []
            for _ in range(2):
                tex = GL.glGenTextures(1)
                GL.glBindTexture(GL.GL_TEXTURE_2D, tex)
                GL.glTexParameteri(GL.GL_TEXTURE_2D,
                                   GL.GL_TEXTURE_MIN_FILTER, GL.GL_NEAREST)
                GL.glTexParameteri(GL.GL_TEXTURE_2D,
                                   GL.GL_TEXTURE_MAG_FILTER, GL.GL_NEAREST)
                GL.glTexParameteri(GL.GL_TEXTURE_2D,
                                   GL.GL_TEXTURE_WRAP_S, GL.GL_CLAMP_TO_EDGE)
                GL.glTexParameteri(GL.GL_TEXTURE_2D,
                                   GL.GL_TEXTURE_WRAP_T, GL.GL_CLAMP_TO_EDGE)
                GL.glTexImage2D(GL.GL_TEXTURE_2D, 0, GL.GL_RGBA8UI, W, H, 0,
                                GL.GL_RGBA_INTEGER, GL.GL_UNSIGNED_BYTE, None)
                self.tex.append(tex)
                glcltex = cl.GLTexture(ctx, cl.mem_flags.READ_WRITE,
                                       GL.GL_TEXTURE_2D, 0, tex)
                self.glcltex.append(glcltex)
            self.clprogram = cl.Program(ctx, kernel).build()
            queue.finish()
            self.execute_cl_load()
    
        def execute_cl_load(self, i=0):
            assert self.clqueue is not None
            cl.enqueue_acquire_gl_objects(self.clqueue, [self.glcltex[i]])
            kernelargs = self.cltex, self.glcltex[i]
            W, H, D = self.data.shape
            self.clprogram.load(self.clqueue, (W, H), None, *kernelargs)
            cl.enqueue_release_gl_objects(self.clqueue, [self.glcltex[i]])
            self.clqueue.finish()
    
        def execute_cl_invert(self, src=0):
            assert src in {0, 1}
            assert self.clqueue is not None
            cl.enqueue_acquire_gl_objects(self.clqueue, self.glcltex)
            kernelargs = self.glcltex[src], self.glcltex[1-src]
            W, H, D = self.data.shape
            self.clprogram.invert(self.clqueue, (W, H), None, *kernelargs)
            cl.enqueue_release_gl_objects(self.clqueue, self.glcltex)
            self.clqueue.finish()
    
        def paintGL(self):
            GL.glClear(GL.GL_COLOR_BUFFER_BIT |
                       GL.GL_DEPTH_BUFFER_BIT |
                       GL.GL_STENCIL_BUFFER_BIT)
            GL.glBindTexture(GL.GL_TEXTURE_2D, self.tex[self.cur_buf])
            GL.glDrawArrays(GL.GL_TRIANGLES, 0, 6)
            GL.glFlush()
            self.ctx.swapBuffers(self.ctx.surface())
    
        def tick(self):
            self.execute_cl_invert(self.cur_buf)
            self.cur_buf = 1 - self.cur_buf
            self.update()
    
        def resizeGL(self, w, h):
            pass
    
    
    def main():
        app = QtWidgets.QApplication(sys.argv)
        signal.signal(signal.SIGINT, lambda *a: app.quit())
        timer = QtCore.QTimer()
        timer.start(200)
        timer.timeout.connect(lambda: 'run interpreter to allow ctrl-c exit')
        window = Window()
        window.resize(800, 600)
        window.show()
        sys.exit(app.exec_())
    
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
