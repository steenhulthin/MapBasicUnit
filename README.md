MapBasicUnit
============

An Unit Test System for MapBasic
--------------------------------

[MapBasic](http://www.mapinfo.com/product/mapinfo-mapbasic/) is language for automating [MapInfo](http://www.mapinfo.com/products/desktop/), which is a desktop [GIS](http://en.wikipedia.org/wiki/Geographic_information_system). 

MapBasicUnit aims to give MapBasic developers a structured way of testing their code that can be automated. 

Usage
-----

1. Create a testrunner .mb file
2. Include the MapBasicUnit.mb
3. Include the .mb file that you want to test
4. Start writing unit test with assertions

*Hopefully this process will be simplified in later versions*

### Create a testrunner .mb file

The basic testrunner:
`Declare Sub Main

Sub Main
Print "-----------"
Print "new testrun." + Time(24)
Print "-----------"
End Sub`

Save the file. The suggested naming convention is test_<name_of_mb_to_test>.mb.

### Include the MapBasicUnit.mb

If MapBasicUnit is located in the same directory as the testrunner:
`Include "MapBasicUnit.mb"

Declare Sub Main

Sub Main
Print "-----------"
Print "new testrun." + Time(24)
Print "-----------"
End Sub`

### Include the .mb file that you want to test

If the .mb that you want to test is located in the same directory as the testrunner:
`Include "MapBasicUnit.mb"
Include "<name_of_mb_to_test>.mb"

Declare Sub Main

Sub Main
Print "-----------"
Print "new testrun." + Time(24)
Print "-----------"
End Sub`


### Start writing unit test with assertions

Let's say that you have a mb file called Trim.mb with the following content:

`Declare Function Trim(Byval word As String) As String

Function Trim(Byval word As String) As String
Trim = LTrim$(RTrim$(word))
End Function`

Then you can write a unit test like this:

`Include "Trim.mb"
Include "MapBasicUnit.mb"

Declare Sub Main

Sub Main
Print "-----------"
Print "new testrun." + Time(24)
Print "-----------"

Call AssertStringEqual("TestThatStringIsTrimmed", "trimmed string", Trim(" trimmed string  "))

End Sub`

In MapInfo the `Message` window will show:
`-----------
new testrun.22:09:07
-----------
Test: TestThatStringIsTrimmed has passed.`
