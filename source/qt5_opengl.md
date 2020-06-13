---
title: qt5_opengl
date: 2020-05-07
---
Example Python program qt5_opengl.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys, ctypes, signal
* from OpenGL import GL, GLU
* from PyQt5 import QtCore, QtGui, QtWidgets

## Classes

* class Window(QtWidgets.QWidget):
* class Widget(QtWidgets.QOpenGLWidget):

## Methods

* def compile_shader(shader):
* def build_draw_program(vertex_shader, fragment_shader):
* def attach_vertices(program, name, data):
* def __init__(self):
* def __init__(self):
* def log_debug_message(self, msg):
* def initializeGL(self):
* def paintGL(self):
* def resizeGL(self, w, h):
* def main():

## Code

Example Python PyQt program :

    import sys, ctypes, signal
    from OpenGL import GL, GLU
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    position_data = (ctypes.c_float*12)(
        -1,-1, 1,-1, -1,1, 1,-1, 1,1, -1,1)
    
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
        
        void main() {
            color = vec4(coord, 1.0, 1.0);
        }
    ''')
    
    def compile_shader(shader):
        shader_type, shader_source = shader
        shader_id = GL.glCreateShader(shader_type)
        GL.glShaderSource(shader_id, shader_source)
        GL.glCompileShader(shader_id)
        compile_status = GL.glGetShaderiv(shader_id, GL.GL_COMPILE_STATUS)
        return shader_id
    
    def build_draw_program(vertex_shader, fragment_shader):
        program = GL.glCreateProgram()
        vertex = compile_shader(vertex_shader)
        fragment = compile_shader(fragment_shader)
        GL.glAttachShader(program, vertex)
        GL.glAttachShader(program, fragment)
        GL.glLinkProgram(program)
        link_status = GL.glGetProgramiv(program, GL.GL_LINK_STATUS)
        return program
    
    def attach_vertices(program, name, data):
        vao = GL.glGenVertexArrays(1)
        GL.glBindVertexArray(vao)
        vbo = GL.glGenBuffers(1)
        GL.glBindBuffer(GL.GL_ARRAY_BUFFER, vbo)
        GL.glBufferData(GL.GL_ARRAY_BUFFER, data, GL.GL_STATIC_DRAW)
        attr = GL.glGetAttribLocation(program, name)
        GL.glEnableVertexAttribArray(attr)
        GL.glVertexAttribPointer(attr, 2, GL.GL_FLOAT, GL.GL_FALSE, 0, None)
    
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
            attach_vertices(draw_program, 'position', position_data)
            
        def paintGL(self):
            GL.glClear(GL.GL_COLOR_BUFFER_BIT |
                       GL.GL_DEPTH_BUFFER_BIT |
                       GL.GL_STENCIL_BUFFER_BIT)
            GL.glDrawArrays(GL.GL_TRIANGLES, 0, 6)
            GL.glFlush()
            self.ctx.swapBuffers(self.ctx.surface())
            
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
