---
layout: post
title: OpenGL Function Calls
date: 2011-07-06 10:20:55.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Labrary
tags: []
meta:
  _edit_last: '1'
  views: '2161'
  bot_views: '3'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/labrary/317.html"
---
<dd>
<strong>Primitives</strong>
<ul>
<li>void <strong>glBegin</strong> (GLenum mode)</li>
<li>void <strong>glEdgeFlag</strong> (GLboolean flag)</li>
<li>void <strong>glEdgeFlagv</strong> (const GLboolean *flag)</li>
<li>void <strong>glEnd</strong> (void)</li>
<li>extern void <strong>glPolygonOffset</strong> (GLfloat factor, GLfloat units)</li>
<li>void <strong>glRect</strong> (TYPE x1, TYPE y1, TYPE x2, TYPE y2)</li>
<li>void <strong>glRectv</strong> (const TYPE *v1, const TYPE *v2)</li>
<li>void <strong>glVertex2</strong> (TYPE x, TYPE y)</li>
<li>void <strong>glVertex3</strong> (TYPE x, TYPE y, TYPE z)</li>
<li>void <strong>glVertex4</strong> (TYPE x, TYPE y, TYPE z, TYPE w)</li>
</ul>
<p> </p>
</dd><dd>
<strong>Vertex Arrays</strong>
<ul>
<li>extern void <strong>glArrayElement</strong> (GLint i)</li>
<li>extern void <strong>glColorPointer</strong> (GLint size, GLenum type, GLsizei stride, const GLvoid *pointer)</li>
<li>extern void <strong>glDisableClientState</strong> (GLenum array)</li>
<li>extern void <strong>glDrawArrays</strong> (GLenum mode, GLint first, GLsizei count)</li>
<li>extern void <strong>glDrawElements</strong> (GLenum mode, GLsizei count, GLenum type, const GLvoid *indices)</li>
<li>extern void <strong>glEdgeFlagPointer</strong> (GLsizei stride, const GLvoid *pointer)</li>
<li>extern void <strong>glEnableClientState</strong> (GLenum array)</li>
<li>extern void <strong>glIndexPointer</strong> (GLenum type, GLsizei stride, const GLvoid *pointer)</li>
<li>extern void <strong>glInterleavedArrays</strong> (GLenum format, GLsizei stride, const GLvoid *pointer)</li>
<li>extern void <strong>glNormalPointer</strong> (GLenum type, GLsizei stride, const GLvoid *pointer)</li>
<li>extern void <strong>glTexCoordPointer</strong> (GLint size, GLenum type, GLsizei stride, const GLvoid *pointer)</li>
<li>extern void <strong>glVertexPointer</strong> (GLint size, GLenum type, GLsizei stride, const GLvoid *pointer)</li>
</ul>
<p><!--more--></p>
</dd><dd>
<strong>Coordinate Transformation</strong>
<ul>
<li>void <strong>glDepthRange</strong> (GLclampd near, GLclampd far)</li>
<li>void <strong>glFrustum</strong> (GLdouble left, GLdouble right, GLdouble bottom, GLdouble top, GLdouble near, GLdouble far)</li>
<li>void <strong>glLoadIdentity</strong> (void)</li>
<li>void <strong>glLoadMatrix</strong> (const TYPE *m)</li>
<li>void <strong>glMatrixMode</strong> (GLenum mode)</li>
<li>void <strong>glMultMatrix</strong> (const TYPE *m)</li>
<li>void <strong>glOrtho</strong> (GLdouble left, GLdouble right, GLdouble bottom, GLdouble top, GLdouble near, GLdouble far)</li>
<li>void <strong>glPopMatrix</strong> (void)</li>
<li>void <strong>glPushMatrix</strong> (void)</li>
<li>void <strong>glRotate</strong> (TYPE angle, TYPE x, TYPE y, TYPE z)</li>
<li>void <strong>glScale</strong> (TYPE x, TYPE y, TYPE z)</li>
<li>void <strong>glTranslate</strong> (TYPE x, TYPE y, TYPE z)</li>
<li>void <strong>glViewport</strong> (GLint x, GLint y, GLsizei width, GLsizei height)</li>
</ul>
<p> </p>
</dd><dd>
<strong>Coloring and Lighting</strong>
<ul>
<li>void <strong>glColor3</strong> (TYPE red, TYPE green, TYPE blue)</li>
<li>void <strong>glColor4</strong> (TYPE red, TYPE green, TYPE blue, TYPE alpha)</li>
<li>void <strong>glColorMaterial</strong> (GLenum face, GLenum mode)</li>
<li>void <strong>glFrontFace</strong> (GLenum dir)</li>
<li>void <strong>glGetLight</strong> (GLenum light, GLenum pname, TYPE *params)</li>
<li>void <strong>glGetMaterial</strong> (GLenum face, GLenum pname, TYPE *params)</li>
<li>void <strong>glIndex</strong> (TYPE index)</li>
<li>void <strong>glLight</strong> (GLenum light, GLenum pname, TYPE param)</li>
<li>void <strong>glLightModel</strong> (GLenum pname, TYPE param)</li>
<li>void <strong>glMaterial</strong> (GLenum face, GLenum pname, TYPE param)</li>
<li>void <strong>glNormal3</strong> (TYPE nx, TYPE ny, TYPE nz)</li>
<li>void <strong>glShadeModel</strong> (GLenum mode)</li>
</ul>
<p> </p>
</dd><dd>
<strong>Clipping</strong>
<ul>
<li>void <strong>glClipPlane</strong> (GLenum plane, const GLdouble *equation)</li>
<li>void <strong>glGetClipPlane</strong> (GLenum plane, GLdouble *equation)</li>
</ul>
<p> </p>
</dd><dd>
<strong>Rasterization</strong>
<ul>
<li>void <strong>glBitmap</strong> (GLsizei width, GLsizei height, GLfloat xorig, GLfloat yorig, GLfloat xmove, GLfloat ymove, const GLubyte *bitmap)</li>
<li>void <strong>glCullFace</strong> (GLenum mode)</li>
<li>void <strong>glGetPolygonStipple</strong> (GLubyte *mask)</li>
<li>void <strong>glLineStipple</strong> (GLint factor, GLushort pattern)</li>
<li>void <strong>glLineWidth</strong> (GLfloat width)</li>
<li>void <strong>glPointSize</strong> (GLfloat size)</li>
<li>void <strong>glPolygonMode</strong> (GLenum face, GLenum mode)</li>
<li>void <strong>glPolygonStipple</strong> (const GLubyte *mask)</li>
<li>void <strong>glRasterPos2</strong> (TYPE x, TYPE y)</li>
<li>void <strong>glRasterPos3</strong> (TYPE x, TYPE y, TYPE z)</li>
<li>void <strong>glRasterPos4</strong> (TYPE x, TYPE y, TYPE z, TYPE w)</li>
</ul>
<p> </p>
</dd><dd>
<strong>Pixel Operations</strong>
<ul>
<li>void <strong>glCopyPixels</strong> (GLint x, GLint y, GLsizei width, GLsizei keight, GLenum type)</li>
<li>void <strong>glDrawPixels</strong> (GLsizei width, GLsizei keight, GLenum format, GLenum type, const GLvoid *pixels)</li>
<li>void <strong>glGetPixelMap</strong> (GLenum map, TYPE *values)</li>
<li>void <strong>glPixelMap</strong> (GLenum map, GLint mapsize, const TYPE *values)</li>
<li>void <strong>glPixelStore</strong> (GLenum pname, TYPE param)</li>
<li>void <strong>glPixelTransfer</strong> (GLenum pname, TYPE param)</li>
<li>void <strong>glPixelZoom</strong> (GLfloat xfactor, GLfloat yfactor)</li>
<li>void <strong>glReadBuffer</strong> (GLenum mode)</li>
<li>void <strong>glReadPixels</strong> (GLint x, GLint y, GLsizei width, GLsizei height, GLenum format, GLenum type, GLvoid *pixels)</li>
</ul>
<p> </p>
</dd><dd>
<strong>Textures</strong>
<ul>
<li>GLboolean <strong>glAreTexturesResident</strong> (GLsizei n, const GLuint *textures, GLboolean *residences)</li>
<li>void <strong>glBindTexture</strong> (GLenum target, GLuint texture)</li>
<li>void <strong>glCopyTexSubimage1D</strong> (GLenum target, GLint level, GLint xoffset, GLint x, GLint y, GLsizei width)</li>
<li>void <strong>glCopyTexSubimage2D</strong> (GLenum target, GLint level, GLint xoffset, GLint yoffset, GLint x, GLint y, GLsizei width, GLsizei height)</li>
<li>void <strong>glCopyTeximage1D</strong> (GLenum target, GLint level, GLenum internalFormat, GLint x, GLint GLsizei v, GLint border)</li>
<li>void <strong>glCopyTeximage2D</strong> (GLenum target, GLint level, GLenum internalFormat, GLint x, GLint, GLsizei width, GLsizei height, GLint border)</li>
<li>void <strong>glDeleteTextures</strong> (GLsizei n, const GLuint *textures)</li>
<li>void <strong>glGenTextures</strong> (GLsizei n, GLuint *textures)</li>
<li>void <strong>glGetTexEnv</strong> (GLenum target, GLenuni pname, TYPE *params)</li>
<li>void <strong>glGetTexGen</strong> (GLenum coord, GLenum pname, TYPE *params)</li>
<li>void <strong>glGetTexLevelParameter</strong> (GLenum targrt, GLint level, GLenum pname, TYPE *params)</li>
<li>void <strong>glGetTexParameter</strong> (GLenum target, GLenum pname, TYPE *params)</li>
<li>void <strong>glGetTeximage</strong> (GLenum target, GLint level, GLenum format, GLenum type, GLvoid *pixels)</li>
<li>void <strong>glIsTexture</strong> (GLuint texture)</li>
<li>void <strong>glPrioritizeTextures</strong> (GLsizei n, const GLuint *textures, const GLclampf *priorities)</li>
<li>void <strong>glTexCoord1</strong> (TYPE s)</li>
<li>void <strong>glTexCoord2</strong> (TYPE s, TYPE t)</li>
<li>void <strong>glTexCoord3</strong> (TYPE s, TYPE t, TYPE r)</li>
<li>void <strong>glTexCoord4</strong> (TYPE s, TYPE t, TYPE r, TYPE q)</li>
<li>void <strong>glTexEnv</strong> (GLenum target, GLenum pname, TYPE param)</li>
<li>void <strong>glTexGen</strong> (GLenum coord, GLenum pname, TYPE param)</li>
<li>void <strong>glTexImage1D</strong> (GLenum target, GLint level, GLint components, GLsizei width, GLint border, GLenum format, GLenum type, const GLvoid *pixels)</li>
<li>void <strong>glTexImage2D</strong> (GLenum target, GLint level, GLint components, GLsizei width, GLsizei height, GLint border, GLenum format, GLenum type, const GLvoid *pixels)</li>
<li>void <strong>glTexParameter</strong> (GLenum target, GLenum pname, TYPE param)</li>
<li>void <strong>glTexSubImage1D</strong> (GLenum target, GLint leve'l, GLint xoffset, GLsizei width, GLenum format, GLenum type, const GLvoid *pixels)</li>
<li>void <strong>glTexSubImage2D</strong> (GLenum target, GLint level, GLint xoffset, GLint yoffset, GLsizei width, GLsizei height, GLenum format, GLenum type, const GLvoid *pixels)</li>
</ul>
<p> </p>
</dd><dd>
<strong>Fog</strong>
<ul>
<li>void <strong>glFog</strong> (GLenum pname, TYPE param)</li>
</ul>
<p> </p>
</dd><dd>
<strong>Frame Buffer Operations</strong>
<ul>
<li>void <strong>glAccum</strong> (GLenum op, GLfloat value)</li>
<li>void <strong>glAlphaFunc</strong> (GLenum func, GLclampf ref)</li>
<li>void <strong>glBlendFunc</strong> (GLenum sfactor, GLenum dfactor)</li>
<li>void <strong>glClear</strong> (GLbitfield mask)</li>
<li>void <strong>glClearAccum</strong> (GLfloat red, GLfloat green, GLfloat blue, GLfloat alpha)</li>
<li>void <strong>glClearColor</strong> ( GLclampf red, GLclampf green, GLclampf blue, GLclampf alpha)</li>
<li>void <strong>glClearDepth</strong> (GLclampd depth)</li>
<li>void <strong>glClearIndex</strong> (GLfloat c)</li>
<li>void <strong>glClearStencil</strong> (GLint s)</li>
<li>void <strong>glColorMask</strong> ( GLboolean red, GLboolean green, GLboolean blue, GLboolean alpha)</li>
<li>void <strong>glDepthFunc</strong> (GLenum func)</li>
<li>void <strong>glDepthMask</strong> (GLboolean flag)</li>
<li>void <strong>glDrawBuffer</strong> (GLenum mode)</li>
<li>void <strong>glIndexMask</strong> (GLuint mask)</li>
<li>void <strong>glLogicOp</strong> (GLenum opcode)</li>
<li>void <strong>glScissor</strong> (GLint x, GLint y, GLsizei width, GLsizei height)</li>
<li>void <strong>glStencilFunc</strong> (GLenum func, GLint ref, GLuint mask)</li>
<li>void <strong>glStencilMask</strong> (GLuint mask)</li>
<li>void <strong>glStencilOp</strong> (GLenum fail, GLenum pass, GLenum zpass)</li>
</ul>
<p> </p>
</dd><dd>
<strong>Evaluators</strong>
<ul>
<li>void <strong>glEvalCoord1</strong> (TYPE u)</li>
<li>void <strong>glEvalCoord2</strong> (TYPE u, TYPE v)</li>
<li>void <strong>glEvalMesh1</strong> (GLenum mode, GLint i1, GLint i2)</li>
<li>void <strong>glEvalMesh2</strong> (GLenum mode, GLint i1, GLint i2, GLint j1, GLint j2)</li>
<li>void <strong>glEvalPoint1</strong> (GLint i)</li>
<li>void <strong>glEvalPoint2</strong> (GLint i, GLint j)</li>
<li>void <strong>glGetMap</strong> (GLenum target, GLenum query, TYPE *v)</li>
<li>void <strong>glMap1</strong> (GLenum target, TYPE u1, TYPE u2, GLint stride, GLint order, const TYPE *points)</li>
<li>void <strong>glMap2</strong> (GLenum target, TYPE u1, TYPE u2, GLint ustride, GLint uorder, TYPE v1, TYPE v2, GLint vstride, GLint vorder, const TYPE *points)</li>
<li>void <strong>glMapGrid1</strong> (GLint n, TYPE u1, TYPE u2)</li>
<li>void <strong>glMapGrid2</strong> (GLint un, TYPE u1, TYPE u2, GLint vn, TYPE v1, TYPE v2)</li>
</ul>
<p> </p>
</dd><dd>
<strong>Selection and Feedback</strong>
<ul>
<li>void <strong>glFeedbackBuffer</strong> (GLsizei size, GLenum type, GLfloat *buffer)</li>
<li>void <strong>glInitNames</strong> (void)</li>
<li>void <strong>glLoadName</strong> (GLuint name)</li>
<li>void <strong>glPassThrough</strong> (GLfloat token)</li>
<li>void <strong>glPopName</strong> (void)</li>
<li>void <strong>glPushName</strong> (GLuint name)</li>
<li>GLint <strong>glRenderMode</strong> (GLenum mode)</li>
<li>void <strong>glSelectBuffer</strong> (GLsizei size, GLuint *buffer)</li>
</ul>
<p> </p>
</dd><dd>
<strong>Display Lists</strong>
<ul>
<li>void <strong>glCallList</strong> (GLuint list)</li>
<li>void <strong>glCallLists</strong> (GLsizei n, GLenum type, const GLvoid *lists)</li>
<li>void <strong>glDeleteLists</strong> (GLuint list, GLsizei range)</li>
<li>void <strong>glEndList</strong> (void)</li>
<li>GLuint <strong>glGenLists</strong> (GLsizei range)</li>
<li>GLboolean <strong>glIsList</strong> (GLuint list)</li>
<li>void <strong>glListBase</strong> (GLuint base)</li>
<li>void <strong>glNewList</strong> (GLuint list, GLenum mode)</li>
</ul>
<p> </p>
</dd><dd>
<strong>Modes and Execution</strong>
<ul>
<li>void <strong>glDisable</strong> (GLenum cap)</li>
<li>void <strong>glEnable</strong> (GLenum cap)</li>
<li>void <strong>glFinish</strong> (void)</li>
<li>void <strong>glFlush</strong> (void)</li>
<li>void <strong>glHint</strong> (GLenum target, GLenum mode)</li>
<li>GLboolean <strong>glIsEnabled</strong> (GLenum cap)</li>
</ul>
<p> </p>
</dd><dd>
<strong>State Queries</strong>
<ul>
<li>void <strong>glGetBooleanv</strong> (GLenum pname, GLboolean *params)</li>
<li>void <strong>glGetDoublev</strong> (GLenum pname, GLdouble *params)</li>
<li>GLenum <strong>glGetError</strong> (void)</li>
<li>void <strong>glGetFloatv</strong> (GLenum pname, GLfloat *params)</li>
<li>void <strong>glGetIntegerv</strong> (GLenum pname, GLint *params)</li>
<li>const GLubyte <strong>*glGetString</strong> (GLenum name)</li>
<li>void <strong>glPopAttrib</strong> (void)</li>
<li>void <strong>glPushAttrib</strong> (GLbitfield mask)</li>
</ul>
</dd>

&nbsp;

Recommend: &nbsp;OpenGL Basics

[https://users.cs.jmu.edu/bernstdh/web/common/lectures/slides\_opengl-basics.php](https://users.cs.jmu.edu/bernstdh/web/common/lectures/slides_opengl-basics.php)

