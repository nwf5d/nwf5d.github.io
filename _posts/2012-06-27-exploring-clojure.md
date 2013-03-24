---
layout: post
title: clojure基础
categories:
- Technology 
tags:
- clojure
- lisp
- language
--- 

Clojure基础：

1. Forms
2. Reader macros
3. Functions
4. Buildings and namespaces
5. Flow control
6. Metadata

# a
# b
# c

* a
* b
* c

| Left align | Right align | Center align |
|:-----------|------------:|:------------:|
| This       |        This |     This     |
| column     |      column |    column    |
| will       |        will |     will     |
| be         |          be |      be      |
| left       |       right |    center    |
| aligned    |     aligned |   aligned    |


|Left align|Right align|Center align|
|:---------|----------:|:----------:|
|This|This|This|
|column|column|column|
|will|will|will|
|be|be|be|
|left|right|center|
|aligned|aligned|aligned|

Clojue code is composed of Clojure data. 
<table>
    <tr>
        <td>Form		Examples			Primary Coverage </td>
    </tr>
</table>
|Form Examples|Primary Coverage
|:----|---:
|Boolean|true,false
|Character |\a 
|Keyword |:tag,:doc
|List |(1,2,3_),(println "foo")
|Map |{:name "Bill", :age 42}
|Nil |nil
|Number |1,4.2
|Set |#{:snap:crackle:pop}
|String |"hello"
|Symbol |user/foo,java.lang.String
|Vector  |[1 2 3]

# Maps,Keywords and Structs
(def inventors {"Lisp" "McCarthy" "Clojure" "Hickey"})
(def inventors {"Lisp" "McCarthy", "Clojure" "Hickey"})

(inventors "Lisp")  =>  "MacCarthy"
(inventors "Foo") => nil

