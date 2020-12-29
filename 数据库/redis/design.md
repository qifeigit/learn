## rehash

redis的hash表会缩容和扩容，会有一个新的空的hash表

原来的hash表我们叫做h0，新的我们叫做h1

在查找时，可能会出现先查找h1，再查找h0



