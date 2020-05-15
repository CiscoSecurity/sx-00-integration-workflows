Logic
=====

.. _variables:

Variables
---------

.. youtube:: Gunp8L7o8pw

Creating Global Variables
^^^^^^^^^^^^^^^^^^^^^^^^^

1. Go to "Variables" on the left hand side to create global variables.

2. To create a new one click the "New Variable" button.

.. image:: _static/newvariable.png
    :target: _static/newvariable.html
    :width: 500px
    :align: center
    :height: 100px

3. Choose a data type. These include boolean, date time, decimal, integer, secure string, string, or you can add a new data type.

.. image:: _static/variabletypes.png
    :target: _static/variabletypes.html
    :width: 400px
    :align: center
    :height: 500px

Example Creation of a String Variable
"""""""""""""""""""""""""""""""""""""

1. Select the type String

2. Provide a display name and a description.

3. Choose a scope for the variable and provide a value.

.. image:: _static/stringvariable.png
    :target: _static/stringvariable.html
    :width: 300px
    :align: center
    :height: 500px

Creating a New Variable Type
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. To create a new variable type go under "Variable Types" and click the "New Variable Type" button.

.. image:: _static/newvariabletype.png
    :target: _static/newvariabletype.html
    :width: 500px
    :align: center
    :height: 100px

2. This creates a structure of the type table and asks for a display name and a description.

3. Add new fields to the variable and click the "Submit" button to create the variable.

4. This new variable type can now be used to create global variables.

.. image:: _static/newtypeinfo.png
    :target: _static/newtypeinfo.html
    :width: 400px
    :align: center
    :height: 400px

Creating Local Variables
""""""""""""""""""""""""

1. To create a local variable click inside the workflow area and go to the properties section on the right.

2. Scroll down until you reach the variables section.

3. Click new variable.

.. image:: _static/localvariable.png
    :target: _static/localvariable.html
    :width: 400px
    :align: center
    :height: 200px

4. Add info for new local variable

.. image:: _static/localvariableinfo.png
    :target: _static/localvariableinfo.html
    :width: 400px
    :align: center
    :height: 500px

Condition Blocks
----------------

Condition blocks allow you to decide which path to take in a workflow.

.. youtube:: alJD8U7dghk

Example Condition Block
^^^^^^^^^^^^^^^^^^^^^^^

This example sets a variable and then runs a python script based on what the value of the variable is.

1. Add the action "Set Variables" followed by a condition block with two of the "Execute Python Script" actions inside.

.. image:: _static/setup.png
    :target: _static/setup.html
    :width: 400px
    :align: center
    :height: 300px

2. Create a local variable for the workflow called "Condition" and make it a boolean and set it to True.

3. Pass the "Set Variables" action the condition variable.

.. image:: _static/condition.png
    :target: _static/condition.html
    :width: 400px
    :align: center
    :height: 300px

4. Click on the left condition branch and click the puzzle piece for the left operand and choose the "Condition" variable we created.

5. Leave the operator as equals and set the right operand to True.

.. image:: _static/leftside.png
    :target: _static/leftside.html
    :width: 400px
    :align: center
    :height: 300px

6. In the left side "Execute Python Script" action add a simple script to print True.

.. image:: _static/true.png
    :target: _static/true.html
    :width: 400px
    :align: center
    :height: 300px

7. Click on the right condition branch and click the puzzle piece for the left operand and choose the "Condition" variable we created.

8. Leave the operator as equals and set the right operand to False.

.. image:: _static/rightside.png
    :target: _static/rightside.html
    :width: 400px
    :align: center
    :height: 300px

9. In the right side "Execute Python Script" action add a simple script to print False.

.. image:: _static/false.png
    :target: _static/false.html
    :width: 400px
    :align: center
    :height: 300px

10. Validate and run the action.

11. The resulting JSON will show the result printed was True as we had the local variable set to True.

.. image:: _static/conditionresult.png
    :target: _static/conditionresult.html
    :width: 400px
    :align: center
    :height: 300px

12. In the workflow you can see which path was taken as it will have a green square around it.

.. image:: _static/greenresult.png
    :target: _static/greenresult.html
    :width: 400px
    :align: center
    :height: 300px

For Each Blocks
---------------

The For Each block allows you to loop through data.

.. youtube:: ivlyzkQnwZ4

Example For Each Block
^^^^^^^^^^^^^^^^^^^^^^

1. Add a For Each block and add the "JSONPathQuery" action to it.

.. image:: _static/foreach.png
    :target: _static/foreach.html
    :width: 300px
    :align: center
    :height: 300px

2. Create a new variable type called Items and populate the table.

.. image:: _static/items.png
    :target: _static/items.html
    :width: 300px
    :align: center
    :height: 300px

3. Click on the For Each block and select the source array to be the items variable by clicking the puzzle piece.

.. image:: _static/sourcearray.png
    :target: _static/sourcearray.html
    :width: 400px
    :align: center
    :height: 300px

4. Click on the "JSONPathQuery" action and select the source JSON to query to be the first item in the table.

.. image:: _static/jsonquery.png
    :target: _static/jsonquery.html
    :width: 400px
    :align: center
    :height: 300px

5. Set the Query to "$", the property name to "ITEM 1", and the property type to "String".

.. image:: _static/jsonvariables.png
    :target: _static/jsonvariables.html
    :width: 400px
    :align: center
    :height: 300px

6. Validate the workflow and run it.

7. After running, you can see that the For Each loop ran 3 times. You can drop down the iterations to see the result of each one.

.. image:: _static/iterations.png
    :target: _static/iterations.html
    :width: 400px
    :align: center
    :height: 300px

8. For the first iteration you can see the item it returned was "desk".

.. image:: _static/resultjson.png
    :target: _static/resultjson.html
    :width: 400px
    :align: center
    :height: 300px

While Loop Blocks
-----------------

A While block will loop until a certain condition is met.

.. youtube:: U_e7DTZCIM8

Example While Loop Block
^^^^^^^^^^^^^^^^^^^^^^^^

1. Start by adding the "Set Variable" action and pass it a local variable called count that is set to zero.

.. image:: _static/count.png
    :target: _static/count.html
    :width: 400px
    :align: center
    :height: 300px

2. Add a While loop block and add the actions "Execute Python Script" and "Set Variable" to the condition branch.

.. image:: _static/whilesetup.png
    :target: _static/whilesetup.html
    :width: 300px
    :align: center
    :height: 300px

3. Add a script to the "Execute Python Script" action to add one to count.

4. Set the script output to be called out.

.. image:: _static/outcount.png
    :target: _static/outcount.html
    :width: 300px
    :align: center
    :height: 300px

5. Set the "Set Variable" action to replace count with the result of the python script.

.. image:: _static/newcount.png
    :target: _static/newcount.html
    :width: 400px
    :align: center
    :height: 300px

6. Set the conditions in the condition branch to use the count variable, not equals, and ten.

.. image:: _static/whilecondition.png
    :target: _static/whilecondition.html
    :width: 400px
    :align: center
    :height: 300px

7. Run the workflow to see that it runs 10 times.

.. image:: _static/run10times.png
    :target: _static/run10times.html
    :width: 400px
    :align: center
    :height: 300px


Parallel Blocks
---------------

Parallel blocks allow you to run two actions concurrently and wait until they both complete before doing the next action.

.. youtube:: fuRjnliRM04

Example Parallel Block
^^^^^^^^^^^^^^^^^^^^^^

1. Start by adding "Create VPC" and "Create Subnet in VPC".

.. image:: _static/startparallel.png
    :target: _static/startparallel.html
    :width: 300px
    :align: center
    :height: 300px

2. Add a parallel block and put both actions in it.

3. Add the "Execute Python Script" after the parallel block.

.. image:: _static/parallelblock.png
    :target: _static/parallelblock.html
    :width: 400px
    :align: center
    :height: 300px

4. When the workflow is run it will run both "Create VPC" and "Create Subnet in VPC" and wait till they are both done before running "Execute Python Script".

5. To add more actions to a parallel block click the plus sign in the top right corner of the block.

.. image:: _static/newblock.png
    :target: _static/newblock.html
    :width: 400px
    :align: center
    :height: 300px
