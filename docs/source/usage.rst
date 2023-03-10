Usage
=====

Installation
------------

To use IREX, first install it using pip:

.. code-block:: console

   pip install -i https://test.pypi.org/simple/ IREX

or
   
.. code-block:: console

   python -m pip install -i https://test.pypi.org/simple/ IREX

Importation
-----------

We recomend to import IREX like this:

.. code-block:: console
   
   from IREX import IREX

Example
-------

First, create an IREX object named IREX, like this:

.. code-block:: console

   IREX = IREX()

With this, you can easily see how IREX's functions works.

Then, we highly recommend to use IREX with the following sequence of functions:

.. code-block:: console

   IREX.load_IREX_datasets()

.. code-block:: console

   IREX.reset() ##For first iteration or
   IREX.iterate() ##For second or greater iteration

.. code-block:: console

   IREX.train_model(do_oversample = True, optimize = False, saveModel = True)

.. code-block:: console

   IREX.evaluate_model()

.. image:: img/evaluate_model.png
  :width: 400

.. code-block:: console

   IREX.run_ALE()

.. image:: img/Ale-bien.png
  :width: 700

.. image:: img/Ale-anomalo.png
  :width: 700

.. code-block:: console

   IREX.apply_Threshold(0.01, -0.01)

.. code-block:: console

   IREX.search_PAI("POSITIVE_CLASS")

.. code-block:: console

   IREX.run_LIME()

.. image:: img/Grupo-1.png
  :width: 1050

.. code-block:: console

   IREX.run_SHAP()

.. image:: img/Grupo-2.png
  :width: 1050

.. code-block:: console

   IREX.precompute_Heatmaps()

.. code-block:: console

   IREX.run_Feature_Importance_Heatmap()

.. image:: img/Grupo-3.png
  :width: 1050

.. code-block:: console

   IREX.run_SHAP_Heatmap()

.. image:: img/Grupo-4.png
  :width: 1050

.. code-block:: console

   IREX.run_LIME_Heatmap()

.. image:: img/Grupo-5.png
  :width: 1050

.. code-block:: console

   IREX.run_ALE_Heatmap()

.. image:: img/Grupo-6.png
  :width: 1050

.. code-block:: console

   IREX.run_Compare_Heatmaps()

.. image:: img/Grupo-7.png
  :width: 1050

.. code-block:: console

   IREX.plot_global_process(['gray', 'black', 'red'])

.. image:: img/Grupo-8.png
  :width: 1050

List of functions
=================

Here are all the functions currently available in the latest IREX version.

load_IREX_datasets
------------------

Loads examples of dataset ready to work with IREX.

set_source_dataset
------------------

-Input parameters:

   -**main_dataset**: the path or name of .csv file which may contain all the questions as columns and all the answers as rows with a final column named "Target" which may contain the final scores of the people who answered the questionnaire.
   
   -**target_classes**: the number and name of the class to which it corresponds. For example:
   
.. code-block:: console

      {0:"Low",1:"Medium",2:"High"}
      
set_expected_answers
--------------------

-Input parameters:
   
   -**source**: the path or name of .csv file which may contain the expected answers of the questionnaire.
   
   -**input_classes**: the number and name of the classification which it refers to. For example:
   
.. code-block:: console

      {0:"Low",1:"High"}
      
reset
-----

Resets the iterative process to start all over again, assigns the local variables for the neural network and also generates the question status and global process dataset.

iterate
-------

Prepares IREX's local variables for the next iteration.

train_model
-----------

Train the prediction model, taking into account these 3 modifiable options:

-**do_oversample**: True or False parameter wich will apply (or not) the SMOTE oversample technique to the samples by calling another function.
   
-**optimize**: True or False parameter wich will optimize (or not) the classification model by calling another function.
   
-**saveModel**: True or False parameter wich will save (or not) the classification model by calling another function.

evaluate_model
--------------

Generates the confusion matrix of the classification model and prints others metrics values such as accuracy, precision, recal, f1-score, support, etc.

run_ALE
-------

Generates ALE graphs for each of the current questions, this contains a slope per class, which represents the way in which the question influences the final ranking. This also creates a dataset wich save the slope values for a future usage.

apply_Threshold
---------------

Use the positive and negative threshold given by the user to identify which items are under these values, tagging them in the dataset which contains the slope values of each question.

-Input parameters:
   
   -**positive**: assigns the positive threshold to use.
   
   -**negative**: assigns the negative threshold to use.

search_PAI
----------

Identifies and tags those questions, that match with the selected mode by the user, in the slopes dataset.

-Available modes:

   -**POSITIVE CLASS**: searches for potentially anomalous items (questions) that may lead to a miss classification on the positive class defined by the user.
   
   -**NEGATIVE_CLASS**: searches for potentially anomalous items (questions) that may lead to a miss classification on the negative class defined by the user.
   
   -**ANY_CLASS**: searches for potentially anomalous items (questions) that may lead to a miss classification in one class OR another.
   
   -**BOTH_CLASSES**: searches for potentially anomalous items (questions) that may lead to a miss classification in both classes.
   
   -**NO_RELEVANT**: searches for potentially anomalous items (questions) that may be between the positive and negative threshold defined by the user.

refine_dataset
--------------

Removes from the local dataset the PAIs (Potentially Anomalous Items) defined by the previous function.

run_LIME
--------

Displays the graphics generated by the LIME XAI method.

run_SHAP
--------

Displays the graphics generated by the SHAP XAI method.

precompute_Heatmaps
-------------------

Prepares the data for the heatmaps generation.

run_Feature_Importance_Heatmap
------------------------------

Displays the heatmaps generated by the Feature Importance XAI method, one per each class and a final graphic whit all heatmaps combined. PAIs are highlighted in red.

run_SHAP_Heatmap
----------------

Displays the heatmaps generated by the SHAP XAI method, one per each class and a final graphic whit all heatmaps combined. PAIs are highlighted in red.

run_LIME_Heatmap
----------------

Displays the heatmaps generated by the LIME XAI method, one per each class and a final graphic whit all heatmaps combined. PAIs are highlighted in red.

run_ALE_Heatmap
---------------

Displays the heatmaps generated by the ALE XAI method, one per each class and a final graphic whit all heatmaps combined. PAIs are highlighted in red.

run_Compare_Heatmaps
--------------------

Displays all the heatmaps generated in the previous functions by the three XAI methods, separated by classes. For this you will need to run the previous three steps.

plot_global_process
-------------------

Displays the different graphics generated to represent the iterative process done. These are: **items used per iteration**, **accuracy per iteration**, **PAIs detected per iteration**, **accuracy and PAIs per iteration**, **recall obtained and anomalous questions detected**.


-Input parameters:
   
   -**plot_colors**: list of colors to use to represent the classes in the **accuracy and PAIs per iteration** and **recall obtained and anomalous questions detected** plot. For example:

.. code-block:: console

      ['gray', 'black', 'red']
