---
layout: post
title: clojure基础
categories:
- Technology 
tags:
- clojure
- lisp
- language

--- Clojure基础：

# Forms
# Reader macros
# Functions
# Buildings and namespaces
# Flow control
# Metadata

Clojue code is composed of Clojure data. 
Form		Examples			Primary Coverage 
Boolean		true,false 
Character	\a 
Keyword		:tag,:doc
List		(1,2,3_),(println "foo")
Map			{:name "Bill", :age 42}
Nil			nil
Number		1,4.2
Set			#{:snap:crackle:pop}
String		"hello"
Symbol		user/foo,java.lang.String
Vector 		[1 2 3]

# Maps,Keywords and Structs
(def inventors {"Lisp" "McCarthy" "Clojure" "Hickey"})
(def inventors {"Lisp" "McCarthy", "Clojure" "Hickey"})

(inventors "Lisp")  =>  "MacCarthy"
(inventors "Foo") => nil

