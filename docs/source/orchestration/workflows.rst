Workflows
=========

Workflows are built with Atomic Actions and they act as lego pieces to create workflows.

Workflows
---------

.. youtube:: 4lcsCGlfwnY

Creating a New Workflow
^^^^^^^^^^^^^^^^^^^^^^^

1. Select the "New Workflow" button.

.. image:: _static/newworkflow.png
    :target: _static/newworkflow.html
    :width: 500px
    :align: center
    :height: 100px

2. Click on the empty palette to see all the properties of the workflow on the right side panel.

3. Provide a display name and a description.

4. Drag an action from the left side panel from any category desired. For an example, we will be using the "AWS Service" named "Create VPC".

.. image:: _static/createvpc.png
    :target: _static/createvpc.html
    :width: 400px
    :align: center
    :height: 400px

5. Click on the action to see the properties required in the right side panel.

6. Click the empty palette and add the AWS Endpoint to the target section under execute on a target.

.. image:: _static/selecttarget.png
    :target: _static/selecttarget.html
    :width: 400px
    :align: center
    :height: 400px

7. Go back to the "Create VPC" action you will see that you can now select the target as use workflow target or you can override it.

.. image:: _static/choosetarget.png
    :target: _static/choosetarget.html
    :width: 400px
    :align: center
    :height: 400px

8. Provide a name tag and an IP address.

.. image:: _static/createvpcinfo.png
    :target: _static/createvpcinfo.html
    :width: 400px
    :align: center
    :height: 500px

9. Add a new action called "Create Subnet in a VPC".

.. image:: _static/createsubnet.png
    :target: _static/createsubnet.html
    :width: 400px
    :align: center
    :height: 500px

10. Provide it a name, an IP CIDR Block, and an availability zone.

.. image:: _static/createsubnetinfo.png
    :target: _static/createsubnetinfo.html
    :width: 400px
    :align: center
    :height: 500px

11. Click the puzzle piece next to VPC ID and go to Activities, Create VPC, and then VPC ID to add the ID.

.. image:: _static/addidvariable.png
    :target: _static/addidvariable.html
    :width: 400px
    :align: center
    :height: 500px

12. The example workflow is now complete.

Running a Workflow from the UI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Click the "Validate" button.

2. Click the "Run" button.

.. image:: _static/runworkflow.png
    :target: _static/runworkflow.html
    :width: 700px
    :align: center
    :height: 100px

Running a Workflow from the API
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following API call can be used to start a workflow

.. code::

    /v1/workflows/start

More information can be found `here <http://na.cloudcenter.cisco.com/orch-ui/swagger-ui/>`_.

Runs
----

Runs allow you to see what actually occurred within your workflow. It lets you see every single step that happened so you can easily see where something went wrong.

.. youtube:: Tu17IclKIlM

How to See Runs
^^^^^^^^^^^^^^^

1. In the left side panel below "Workflows" you will see a tab for "Runs".

.. image:: _static/runs.png
    :target: _static/runs.html
    :width: 550px
    :align: center
    :height: 200px

2. Find runs for a specific workflow by going to the workflow and hitting the "View Runs" button.

.. image:: _static/specificrun.png
    :target: _static/specificrun.html
    :width: 700px
    :align: center
    :height: 50px

3. The runs page will show you the status of the run, the time it was started, the time it ended, the user it was started by, and the owner of the workflow.

.. image:: _static/status.png
    :target: _static/status.html
    :width: 700px
    :align: center
    :height: 100px

4. Use the filter on the left to see specific results and workflows.

.. image:: _static/filter.png
    :target: _static/filter.html
    :width: 400px
    :align: center
    :height: 600px

How to View a Failed Run
^^^^^^^^^^^^^^^^^^^^^^^^

1. Click on a workflow that failed it will take you to the workflow and put a green box around everything that ran successfully and a red box around what failed.

2. Click on the red box and see what all the input and output was to find the error.

.. image:: _static/failedrun.png
    :target: _static/failedrun.html
    :width: 600px
    :align: center
    :height: 600px

.. _targets:

Targets
-------

Targets specify where you want your actions or workflows to run. There are both single targets or target groups to choose from.

.. youtube:: OeBlb6fj760

Creating Single Targets
^^^^^^^^^^^^^^^^^^^^^^^

1. Create a new single target click the "New Target" button.

.. image:: _static/newtarget.png
    :target: _static/newtarget.html
    :width: 500px
    :align: center
    :height: 100px

2. Choose a target type.

.. note::

    HTTP Endpoint is the most common target type.

.. image:: _static/targettype.png
    :target: _static/targettype.html
    :width: 400px
    :align: center
    :height: 400px

3. Create a display name and description.

4. Choose to apply an account key or create a new one.

.. note::

    Account keys are only required for actions that require authentication.

5. Provide the HTTP protocol, host/ip address, the port, and the path.

.. image:: _static/targetinfo.png
    :target: _static/targetinfo.html
    :width: 400px
    :align: center
    :height: 700px

6. Click the "Submit" button.

Adding Targets to a Workflow
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Open the workflow.

2. Select the target you created.

.. image:: _static/addtarget.png
    :target: _static/addtarget.html
    :width: 400px
    :align: center
    :height: 400px


Creating Target Groups
^^^^^^^^^^^^^^^^^^^^^^

TODO add info here

.. _account_keys:

Account Keys
^^^^^^^^^^^^

Account keys are used to authenticate to a target that is used in workflows. Account keys can be credentials like usernames and passwords or they can be certificates.

.. youtube:: pM2jKpDAJlo

Creating a New Account Key
""""""""""""""""""""""""""

1. Click on the "New Account Key" button.

.. image:: _static/accountkeybutton.png
    :target: _static/accountkeybutton.html
    :width: 500px
    :align: center
    :height: 200px

2. Choose the target account key type.

.. image:: _static/keytype.png
    :target: _static/keytype.html
    :width: 400px
    :align: center
    :height: 500px

.. note::

    The most common key type is HTTP Basic Authentication or HTTP Client Certificate Authentication. Most REST interfaces will use HTTP Basic Authentication.

Example of Creating New Account Keys
""""""""""""""""""""""""""""""""""""

1. To create a HTTP Basic Authentication Key you will provide a display name and a description. Then you will add the credentials and click the "Submit" button.

.. image:: _static/httpkey.png
    :target: _static/httpkey.html
    :width: 400px
    :align: center
    :height: 500px

2. To create an Email Credentials Key you will provide a display name and a description. Then you will provide a from email address and a password then click the "Submit" button.

.. image:: _static/emailkey.png
    :target: _static/emailkey.html
    :width: 400px
    :align: center
    :height: 500px

3. To create a SNMP Credentials Key you will provide a display name and a description. Then you will provide a version number, a username, and a security level then click the "Submit" button.

.. image:: _static/snmpkey.png
    :target: _static/snmpkey.html
    :width: 400px
    :align: center
    :height: 500px

Using an Account Key
""""""""""""""""""""

1. Under "Targets" you can choose a target and apply an account key you created to it.

.. image:: _static/newkeytarget.png
    :target: _static/newkeytarget.html
    :width: 400px
    :align: center
    :height: 700px

.. _atomic_actions:

Atomic Actions
--------------

Atomic actions are the building blocks of workflows.

.. youtube:: r-1LTqU4RWI

Creating an Example Atomic Action
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This atomic action will call out a postman echo and echo the response back to us.

Postman Echo
""""""""""""

1. Start by clicking the "New Workflow" button.

.. image:: _static/newworkflow.png
    :target: _static/newworkflow.html
    :width: 500px
    :align: center
    :height: 100px

2. Scroll down in the left side bar until you reach "Web Service" and add a "HTTP Request" to the workflow.

.. image:: _static/newecho.png
    :target: _static/newecho.html
    :width: 400px
    :align: center
    :height: 400px

3. Provide the HTTP Request the display name "Postman Echo" and provide a description.

4. Provide the relative URL "/get".

.. image:: _static/getURL.png
    :target: _static/getURL.html
    :width: 400px
    :align: center
    :height: 400px

5. Go to the target section and select execute on a target.

6. Create a new target called "Postman Echo" and provide it the URL "postman-echo.com".

.. image:: _static/echotarget.png
    :target: _static/echotarget.html
    :width: 400px
    :align: center
    :height: 400px

7. To test the request please change "/get" to "/get?test&test2" then validate the workflow and run it. In the response JSON you will be able to see "test", "test2", and some unnecessary data.

Removing Unnecessary JSON
^^^^^^^^^^^^^^^^^^^^^^^^^

1. To remove the extra unnecessary JSON add another action called "JSONPathQuery". This allows you to pick which data you want to be returned back.

.. image:: _static/jsonpath.png
    :target: _static/jsonpath.html
    :width: 400px
    :align: center
    :height: 400px

2. In the right hand bar scroll down to JSON Query and click the puzzle piece to add a source JSON to query.

3. Click activities then "Postman Echo" then choose the body.

.. image:: _static/jsonvariable.png
    :target: _static/jsonvariable.html
    :width: 400px
    :align: center
    :height: 400px

4. Add a JSON Path Query by providing "$.args" and the property name "args".

5. To test this action validate the workflow and run it. If you look at the response from the "JSONPathQuery" you will just see "test" and "test2".

Making the Workflow Reusable
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Click an empty spot on the screen and then add a variable.

2. Choose the data type string, add a display name of "Args", choose the scope to be input, and make it required.

.. image:: _static/args.png
    :target: _static/args.html
    :width: 400px
    :align: center
    :height: 400px

3. Go back to the "Postman Echo" action and change the "/get?test&test2" by leaving the "/get?" and clicking the puzzle piece to select the variable you made.

.. image:: _static/selectargs.png
    :target: _static/selectargs.html
    :width: 400px
    :align: center
    :height: 400px

4. Set an output variable by adding a "Set Variables" action to the workflow.

.. image:: _static/setvariableecho.png
    :target: _static/setvariableecho.html
    :width: 400px
    :align: center
    :height: 400px

5. Go back to the main options for the workflow and add a new variable of type string called "OutArgs" and change the scope to output.

.. image:: _static/outargs.png
    :target: _static/outargs.html
    :width: 400px
    :align: center
    :height: 400px

6. Add the variable to the "Set Variables" action by clicking the puzzle piece and choosing "OutArgs" for the variable to update section and for the variable value new section select JSONPath Query then Jsonpath Queries then args.

7. Validate the workflow and select the "Is Atomic Workflow" button and give it a group name.

.. image:: _static/atomicworkflow.png
    :target: _static/atomicworkflow.html
    :width: 400px
    :align: center
    :height: 100px

8. Validate the workflow again and you can no longer click run.

9. To use the "Postman Echo" workflow you can create a new workflow and now add the "Postman Echo" action.



