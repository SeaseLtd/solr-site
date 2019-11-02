Title: Features
URL: pylucene/
save_as: pylucene/features.html
template: pylucene/page
slug: pylucene-features

## Warning

Before calling any PyLucene API that requires the Java VM, start it by
calling <i>initVM(classpath, ...)</i>.
More about this function in <a href="jcc/features.html">here</a>.

##Installing PyLucene

PyLucene is a Python extension built with
<a href="jcc/">JCC</a>.


To build PyLucene, JCC needs to be built first. Sources for JCC are
included with the PyLucene sources. Instructions for building and
installing JCC are <a href="jcc/install.html">here</a>.


Instruction for building PyLucene
are <a href="install.html">here</a>.



##API documentation

PyLucene is closely tracking Java Lucene<span style="vertical-align: super; font-size: xx-small">TM</span> releases. It intends to
supports the entire Lucene API.


PyLucene also includes a number of Lucene contrib packages: the
Snowball analyzer and stemmers, the highlighter package, analyzers
for other languages than english, regular expression queries,
specialized queries such as 'more like this' and more.


This document only covers the pythonic extensions to Lucene offered
by PyLucene as well as some differences between the Java and Python
APIs. For the documentation on Java Lucene APIs,
see <a href="https://lucene.apache.org/java/docs/api/index.html">here</a>.


To help with debugging and to support some Lucene APIs, PyLucene also
exposes some Java runtime APIs.


##Samples

The best way to learn PyLucene is to look at the samples and tests
included with the PyLucene source release or on the web at:


- <a href="https://svn.apache.org/viewcvs.cgi/lucene/pylucene/trunk/samples">https://svn.apache.org/viewcvs.cgi/lucene/pylucene/trunk/samples</a>

- <a href="https://svn.apache.org/viewcvs.cgi/lucene/pylucene/trunk/test">https://svn.apache.org/viewcvs.cgi/lucene/pylucene/trunk/test</a>



##Threading support with attachCurrentThread

Before PyLucene APIs can be used from a thread other than the main
thread that was not created by the Java Runtime, the
<i>attachCurrentThread()</i> method must be called on the
<i>JCCEnv</i> object returned by the <i>initVM()</i>
or <i>getVMEnv()</i> functions.



##Exception handling with lucene.JavaError

Java exceptions are caught at the language barrier and reported to
Python by raising a JavaError instance whose args tuple contains the
actual Java Exception instance.



##Handling Java arrays

Java arrays are returned to Python in a <i>JArray</i>
wrapper instance that implements the Python sequence protocol. It
is possible to change array elements but not to change the array
size.


A few Lucene APIs take array arguments and expect values to be
returned in them. To call such an API and be able to retrieve the
array values after the call, a Java array needs to instantiated
first.<br/>
For example, accessing termDocs:

<code>
termDocs = reader.termDocs(Term("isbn", isbn))<br/>
docs = JArray('int')(1)   # allocate an int[1] array<br/>
freq = JArray('int')(1)   # allocate an int[1] array<br/>
if termDocs.read(docs, freq) == 1:<br/>
&nbsp;&nbsp;bits.set(docs[0])     # access the array's first element<br/>
</code>

In addition to <i>int</i>, the <i>JArray</i>
function accepts <i>object</i>, <i>string</i>,
<i>bool</i>, <i>byte</i>, <i>char</i>,
<i>double</i>, <i>float</i>, <i>long</i>
and <i>short</i> to create an array of the corresponding
type. The <i>JArray('object')</i> constructor takes a second
argument denoting the class of the object elements. This argument
is optional and defaults to Object.


To convert a char array to a Python string use a
<i>''.join(array)</i> construct.


Instead of an integer denoting the size of the desired Java array,
a sequence of objects of the expected element type may be passed
in to the array constructor.<br/>
For example:

<code>
\# creating a Java array of double from the [1.5, 2.5] list<br/>
JArray('double')([1.5, 2.5])<br/>
</code>

All methods that expect an array also accept a sequence of Python
objects of the expected element type. If no values are expected
from the array arguments after the call, it is hence not necessary
to instantiate a Java array to make such calls.


See <a href="jcc/features.html">JCC</a> for more
information about handling arrays.



##Differences between the Java Lucene and PyLucene APIs

- The PyLucene API exposes all Java Lucene classes in a flat namespace
in the PyLucene module. For example, the Java import
statement <code>import
org.apache.lucene.index.IndexReader;</code> corresponds to the
Python import statement <code>from lucene import
IndexReader</code>

- Downcasting is a common operation in Java but not a concept in
Python. Because the wrapper objects implementing exactly the
APIs of the declared type of the wrapped object, all classes
implement two class methods called instance_ and cast_ that
verify and cast an instance respectively.




##Pythonic extensions to the Java Lucene APIs

Java is a very verbose language. Python, on the other hand, offers
many syntactically attractive constructs for iteration, property
access, etc... As the Java Lucene samples from the <em>Lucene in
Action</em> book were ported to Python, PyLucene received a number
of pythonic extensions listed here:


- Iterating search hits is a very common operation. Hits instances
are iterable in Python. Two values are returned for each
iteration, the zero-based number of the document in the Hits
instance and the document instance itself.<br/>
The Java loop:
<code>
for (int i = 0; i &lt; hits.length(); i++) {<br/>
&nbsp;&nbsp;Document doc = hits.doc(i);<br/>
&nbsp;&nbsp;System.out.println(hits.score(i) + " : " + doc.get("title"));<br/>
}<br/>
</code>
can be written in Python:
<code>
for hit in hits:<br/>
&nbsp;&nbsp;hit = Hit.cast_(hit)<br/>
&nbsp;&nbsp;print hit.getScore(), ':', hit.getDocument['title']<br/>
</code>
if hit.iterator()'s next() method were declared to return
<i>Hit</i> instead of <i>Object</i>, the above
cast_() call would not be unnecessary.<br/>
The same java loop can also be written:
<code>
for i xrange(len(hits)):<br/>
&nbsp;&nbsp;print hits.score(i), ':', hits[i]['title']<br/>
</code>

- Hits instances partially implement the Python 'sequence'
protocol.<br/>
The Java expressions:
<code>
hits.length();<br/>
doc = hits.get(i);<br/>
</code>
are better written in Python:
<code>
len(hits)<br/>
doc = hits[i]<br/>
</code>

- Document instances have fields whose values can be accessed
through the mapping protocol.<br/>
The Java expression:
<code>
doc.get("title")
</code>
is better written in Python:
<code>
doc['title']
</code>

- Document instances can be iterated over for their fields.<br/>
The Java loop:
<code>
Enumeration fields = doc.getFields();<br/>
while (fields.hasMoreElements()) {<br/>
&nbsp;&nbsp;Field field = (Field) fields.nextElement();<br/>
&nbsp;&nbsp;...<br/>
}<br/>
</code>
is better written in Python:
<code>
for field in doc.getFields():<br/>
&nbsp;&nbsp;field = Field.cast_(field)<br/>
&nbsp;&nbsp;...<br/>
</code>
Once JCC heeds Java 1.5 type parameters and once Java Lucene
makes use of them, such casting should become unncessary.




##Extending Java Lucene classes from Python

Many areas of the Lucene API expect the programmer to provide
their own implementation or specialization of a feature where
the default is inappropriate. For example, text analyzers and
tokenizers are an area where many parameters and environmental
or cultural factors are calling for customization.


PyLucene enables this by providing Java extension points listed
below that serve as proxies for Java to call back into the
Python implementations of these customizations.


These extension points are simple Java classes that JCC
generates the native C++ implementations for. It is easy to add
more such extensions classes into the 'java' directory of the
PyLucene source tree.


To learn more about this topic, please refer to the JCC
<a href="jcc/features.html">documentation</a>.


Please refer to the classes in the 'java' tree for currently
available extension points. Examples of uses of these extension
points are to be found in PyLucene's unit tests.