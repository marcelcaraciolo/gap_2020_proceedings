:author: Marcel Pinheiro Caraciolo
:email: marcel.caraciolo@einstein.br
:institution: Hospital Israelita Albert Einstein

:author: Juliano M Borges
:email: 	jmb2@cesar.org.br
:institution: Cesar School

-----------------------------------------------------------------
Continuous Improvement For Clinical Bioinformatics Pipelines
-----------------------------------------------------------------

.. class:: abstract

   How to successfully build a bioinformatics pipeline for clinical sequencing exams, consisting of collecting and refining requirements,
   interative software development, continuous testing and validation, and delivery, is the challenge faced by many bioinformatics development teams.
   Typical pipeline involves collecting and refining the requirements, translating into features, setting up an infrastructure, building a computation
   process, and analyzing the results. When the adjustments are made, this process repeates as many times as necessary until the pipeline has been properly
   validated. At Varstation, by using continous improvement techniques, we built a more efficient way to iterate on building those pipelines so we could optimize
   and deliver them faster, but commited to providing accurate tests results. In this paper, we present our approach for design, build and deliver our
   pipelines after several changes in our software development process, which can be valuable for any bioinformatics teams 
   interested in implementing with faster iterations clinical bioinformatics pipelines.   

   

.. class:: keywords

   bioinformatics pipelines, clinical NGS, continous improvement, software development, continuous integration, continuous delivery, devops practices

Introduction
------------

Bioinformatics has become an important component in clinical laboratories generating, analyzing, maintaining, and interpreting data from molecular genetics testing.
Given the rapid adoption of NGS-based clinical testing, service providers must develop informatics workflows that adhere to the rigor of clinical laboratory standards,
but flexible to changes as the chemistry and software for analyzing sequencing data mature. Next generation sequencing (NGS) is a transformative technology that is redefining the landscape
of human molecular genetic testing. It enables unprecedented parallelization of sequencing reactions, facilitating highly multiplexed testing paradigms with relatively rapid turnaround
time and decreasing costs. A growing number of diagnostic laboratories are embracing NGS and using it to drive new DNA-based test offerings, ranging in size and species, from human to
microbiome genomes and from multigene disease-specific panels to use of complete genome sequencing. When genetic tests are ordered, there is probably little thought as to all of the of bioinformatics work required
to make the test possible. The Hospital Israelita Albert Einstein provides diagnostic tests to help physicians understand risk profiles, diagnose medical conditions, or inform treatment decisions. To support their
comprehensive test menu and commitment to providing timely and accurate test results, the bioinformatics team focuses on optimizing their pipelines by designing workflows to leverage modularity and computational re-use, in order to
better understand the requirements for each molecular test; by using declarative workflow language as main programming tool to a more collaborative and legible code; by applying continous integration systems to the software development
in order to avoid manual validation, integration tests and releases; and by creating a collaborative repository of guidelines so any bioinformatician starting working at our team, can easily begin build his first pipelines.
All these improvements were conducted during three months by observing the bioinformatics pipeline development organization and applying changes in order to evaluate the gains in each step of the bioinformatics development lifecycle.

The purpose of this paper is to present an experience report in our bioinformatics team at Varstation (our bioinformatics department at the hospital), by providing a collection of experience notes, artifacts and systems that we introduced
and formalized during the period of reviewing our bioinformatics software development process. The detailed study results can be found in the remainder of the paper.
This paper is structured as follows. Section II introduces the background and related work that indicate the reason for our research. Section III introduces the research method
and process. Section IV presents the artifacts produced and related results. Section V discusses the implications to study results and threats to validity. Section VI concludes the study and illustrates the future work.

II. Background
--------------

This section reviews the concept of bioinformatics development lifecycle and related work conducted on our continous improvement research.


Bioinformatics pipeline development
===================================

With the advent of clinical sequencing , the bioinformatis pipelines for detection and variant annotation are becoming more popular. However, the process of translating the requirements of the biological and medical specialists is not a trivial task, adding to that,
the continuous development, testing and release, with improvements, the clinical pipelines. Compared to the traditional software development, the bioinformatics pipelines handles with biological inputs/outputs, runtime parameters and code itself, and  requires a continous
monitoring as the new versions from the dependant softwares are released or a need for a replacement of a new annotation biological database or even a new type of variant that must be detected. In our scenario the bioinformatics pipeline must be reavaluated every time 
that a new genome version is updated or any refreshments in related databases. Developing a bioinformatics pipeline includes five steps from its conception to the final release in the production environment. At the figure :ref:`egfig` we depict the bioinformatics pipeline development lifecycle.

.. figure:: figure1.png

   The commom bioinformatics clinical pipeline development lifecycle. Each step in this workflow must be consolidated with the inputs/outputs mandatory for the following steps.  :label:`egfig` 

.. figure:: figure1.png
   :align: center
   :figclass: w


The analysis pipeline is typically considered to comprise the five main steps of plan/design, build, test/optimization, validation, and release/deploy. The planning includes the biological problem understanding and the selection of the components required to build the pipeline. The 
build stage leads to bioinformatics pipeline development including the coding, testing and code styles standardization. The test/optimization occurs when the pipeline is built successfully and it must be evaluated considering secondary requirements such as performance and scale.  
The validation may include the validation and benchmarking of the pipeline in order to guarantee the minimum defined performance metrics criteria. Finally, the release step is when the final artifacts must be delivered considering factors of versioning, docummentation and the executable
binary to be deployed in the production environment. This general framework varies depending on the precise analytical application, and successful clinical implementation of such work flows requires extensive expertise in bioinformatics and clinical regulatory issues.

Continuous Improvement
=======================

Continuous Improvement related topics have been studied by software engineering (SE) practitioners and researchers for many years. There are several related articles in blogs,
magazine, SE releated magazines. Continuous Improvement identifies the opportunities to streamline the work while reducing waste. It follows the Japanese concept of kaizen, which means to make small incremental improvements continuously. It empowers the agile team so
they can work well together and discuss what is working and what isn’t. There are several empirical studies and practices of conducting continous improvement in software organizations. However, despite these practices have been examined by in many software industries, we failed
to identify any research conducted on healtchare and bioinformatics software organizations that are carrying continous improvement in practices.

Product Canvas: Building the pipelines with the right features
==============================================================

The goal of developing the product canvas has been to create a lean tool to develop successful product models in a framework that integrates user experience and feature development themes,
encourages innovation, and more closely represents the process as it occurs in practice.  Specifically, it combines Agile and UX by complementing user stories with personas, storyboards, scenarios, design sketches and other UX artifacts.
The prototype version of the product canvas is shown in Figure :ref:`egfig2` below and is available online for developers and practitioners to test, evaluate, and provide feedback. In our scenario, this tool can be applied to prepare and gather required 
information to the pipeline development phase as a product with a specific goal defined and the target genetic testing identified by the clinical specialists. From the laboratory need it is also possible to derive the validation metrics and 
required acceptance criteria.

.. figure:: figure2.png

   The Product Canvas is a collaborative tool that combines Agile and UX by complementing user stories with personas, storyboards, scenarios, design sketches and other UX artifacts. It helps the team
   to identify the target group, extracting their needs and solving those needs with solutions and finally packaging those solutions as tasks.  :label:`egfig2` 

.. figure:: figure2.png
   :align: center
   :figclass: w


Workflow Description Language for building pipelines
====================================================

One of the key challenges for bioinformatics pipelines is the rapidly increasing number and complexity of analytical methods. Reproducing the results of a bioinformatics workflow can be challenging given the number of components, each having its own
set of parameters, dependencies, supporting files, and installation requirements. Several platforms currently exist for the design and execution of complex pipelines. Unfortunately, current platforms
lack the necessary combination of parallelism, portability, flexibility and/or reproducibility that are required by the current research environment. To address these shortcomings, workflow pipelines that provide
a platform to develop and share portable pipelines have recently arisen. Workflows descriptors such as Workflow Description Language (WDL) are hosted with containers to provide workflows scripts that can be reproducibly
executed on the cloud or local cluster. In our team, we migrated our pipelines written in bash scripts to WDL in order to improve our pipeline development step and facilitate our bioinformaticians to rapidly start developing.

Continous integration
=======================

Continuous integration (CI) has been a de facto standard for building industrial-strength software. Yet, there is little attention towards
applying CI to the development of bioinformatics applications until the very recent effort on the theoretical side. Continuous integration helps the development team to automate several steps of the pipeline development lifecycle such as
the test automation, the validation benchmark against a test sample, or the promotion of the release pipeline artfifact which can be used for upstream consumption in the production environment.

Figure :ref:`egfig3` presents an overview of the software development lifecycle under a traditicional CI system. The entire lifecycle consists of four stages: develop, build, test and merge. In advanced scenarios the CI workflow can also be added to 
a continous delivery (CD) when the release artifact is automatically released to the repository , or even further, to a continuous deployment, when in this case the artifact is deployed automatically to the production environment.

.. figure:: figure3.png

   The development lifecycle in the framework of traditional software development.  :label:`egfig3`

.. figure:: figure3.png
   :scale: 20%
   :figclass: bht


Development Playbooks
=====================

The bioinformatics team is a multidisciplinary group that may include developers, devops developers, designers , biologists and bioinformaticians who have different cultures, terminologies, and standards of proficience. Thus, in order to establish a productive collaboration and
effective development, the team must have the necessary tools, proper training and the best practices in mind, before starting building the pipelines. Development playbooks are intervention guidebooks that are created by, understood by, and acceptable to all members of the
multidisciplinary bioinformatices development team. These guidelines are created to aid the development of any software, so the beginners and the experienced members can use the same development principles and definitions shared to improve their target goal, which is the
delivery of a reproducible, tested and optimized pipeline. Development playbooks are very popular among several mature software companies that are evolving their software development skills.


III. Research Method
--------------------

We conducted our continous improvement process in four stages: (1) observation, (2) planning, (3) execution, (4) review . It is based on the Plan-Do-Check-Act (PDCA) cycle. Each stage is described in the following sub-sections.



A. Observation
===============

We reviewed the current bioinformatics variant calling pipeline development process and discussed with the team members the pain points for each stage. All these interviews and meetings during the retrospective and daily meetings at the scrum cerimonies helped us to gather
data to perform some initatives and modifications in the process.

B. Planning
===========

With the experience notes, the team reflection reports, and the software production snapshot data carried from the first step, we analysed all those material and identified some improvements that could be performed at our process. 
Each improvement was first discussed with the team, since the implementation of some these adjustments needed a timebox in their current product development sprints. These materials were transformed in user stories or epics in our 
backlog so we could implement and test them throhgh the sprint.


C. Execution
============

The user stories were put into the sprint backlog accordingly to the slots available negotiated with the product owner and the development team. Some changes were just improvements in docummentation,
others just an automation in a specific development build stage (using CIs for instance). The team was commited to perform these changes since it would bring already new experiences and learnings about our current process.



D. Review
==========

This is the last stage, where we collected the feedback about the improvements after the improvements, and made new adjustments as we decided to refine it, or sometimes since it could be a complex task, delay it for a future iteration.
The review technique also helped us to identify inneficiencies to eliminate, positive things to enhance and new opportunities to improve.




IV. Current Results
-------------------

In this section we provide some of the current results and the artifacts produced during the period of three months (from August 2021 until October 2021) as we started the study method presented in the section above.


A. Design and Planning
======================

Our bioinformatics team, through the years, was delivering bioinformatics pipelines for many omics: transcriptome, genomics and metagenomics. For each one there is a common toolset for the pipeline building development. It is up to the bioinformatician to analyze the biological
problem that will be solved, define the tools and algorithms available for each variant calling step from the DNA digital sequences to the genomic variants and build an automated pipeline that perform all these tasks using the computational resources. During the design and Planning
stage our team discuss with our clients (medical specialists and biologists) to have a common and clear understanding about the main requirements for the pipeline that will be associated to a research project or a novel genetic test available for our patients. Inspired by the 
Product Canvas , explained at our background section, we proposed and created a Bioinformatics Pipeline Canvas (BPC).  Our canvas is a collaborative tool that includes Agile , scientific methdology, adapted to facilitate the technical discussions between our bioinformaticians, biologist
and geneticists. The main goal is to have an overall picture to model the pipeline. We will use it as a validation method for checking all the requirements to have a pipeline implemented: Which are the inputs/outs expected for each step of the pipeline, the tools required for
each pipeline component (task) and the performance criteria that will be considered before being released to a production environment.

At the figure :ref:`egfig4` , we show an example of a full-filled canvas in one of our internal trainings. The artifact is available as open-source template at the website miro.com.


.. figure:: figure4.png

   Our Bioinformatics Pipeline Canvas, inspired by the Product Canvas as a visual tool for our developers and product owners to facilitate and translate the clinical and biological requirements into features, expected inputs and outputs and
   performance metrics criteria.  :label:`egfig4` 

.. figure:: figure4.png
   :align: center
   :figclass: w


B. Development
==============

One of the improvements at our development cycle was to rethink how we managed and orchestrated our current variant calling bioinformatics pipelines. The changing landscape of genomics research and clinical practice
has created a need for computational pipelines capable of efficiently orchestrating complex analysis stages while handling large volumes of data across heterogeneous computational environments. Our current pipelines
were monolytical with shared command line bash scripts with python/perl/R code invoked. The main issue in this approach is that it is difficult to identify/debug problems, it doesn't enable a rapid escalation and
doesn't promote the modularity within the pipelines. Since 2020 we started to discuss novel tools and bioinformatics worfklow programming languages to help us to mitigate these problems. After several proof-of-concept tests (POCs)
and discussions we came to workflow tools, such as WDL (Workflow Description Language), that makes pipelines easier to express and build. With WDL, you can easily describe the module dependencies and track version changes to the workflow.
Our team reorganized the pipelines and broke the code within them into smaller modules in WDL, so our future pipelines could benefit of the components implemented just plugging it into the main WDL workflow, and just modify the corresponding
input files By reusing the tasks , developers can dramatically speed the development of new workflows. The figures :ref:`egfig5` and :ref:`egfig6` presents the architecture overview of bioinformatics workflow written in modules and
the WDL declarative syntax and style code, respectively.


.. figure:: figure5.png

   Bioinformatics workflows written with WDL in multiple levels of complexity warrant a modular construction. It is easiest to program the workflow when its logic is abstracted away (in Tasks, red)
   from the command line invocations (in Bash scripts, pink) of the bioinformatics tools (light pink). Individual workflows can be further used as subworkflows of a larger Master
   workflow. This architecture facilitates expression of additional complexity due to optional modules(dashed line), nested levels of parallelism (groups of arrows connecting red rectangles) 
   and scatter-gather patterns (task 2 scattered across samples being merged into task 3). :label:`egfig5`


.. figure:: figure5.png
   :align: center
   :figclass: w


.. figure:: figure6.png

   Example of an workflow skeleton. We define the inputs and corresponding outputs, each one declared as variables. We also define the tasks, which it will be computational blocks that will execute the pipeline commands.
   These tasks are invoked from the main workflow using the call methods. :label:`egfig6`


.. figure:: figure6.png
   :align: center
   :figclass: w

The team also changed the orchestration tool from using AWS Lambda tasks to a open source bioinformatics tool developed by the Broad Institute of Harvard University and MIT called Cromwell.
It is a workflow-execution engine that simplifies the orchestration of computing tasks needed for genomic analysis. With the infra-structure and devops team working together, we led to Cromwell
being able to run directly on an Amazon Web Services (AWS, cloud-computing) environment. This has given our bioinformatician more flexibility in scaling their genomic workflows.
For instance, Our Whole Human Genome Variant Calling Pipeline is using Cromwell to automate and enhance its quality control capabilities in our analysis software Varstation. Figure :ref:`egfig7` presents
the AWS proposed architecture for running Cromwell using the AWS Batch environment.


.. figure:: figure7.png

   Cromwell is a workflow management system for scientific workflows developed by the Broad Institute and supports job execution using AWS Batch. :label:`egfig7`


.. figure:: figure7.png
   :align: center
   :figclass: w

Finally, one of the improvements for building new bioinformatics pipelines was propose a minimal base template for our developers getting started following our best practices and guidelines. Several CI scripts, version control management,
docummentation build scripts and automated workflow test suite integrated were compiled into this repository. It is a basic start pipeline so from begginners to advanced users can use it right away. Until the date of publishing of this paper, we
were still validating the framework by migrating our old pipelines to WDL based on it. The figure :ref:`egfig8` shows the repository of our minimal pipeline template hosted as a template repository on Github.

.. figure:: figure8.png

   Our minimal pipeline template was hosted in Github as a pipeline repository so the developers can easily fork all the code to their new pipeline repository. :label:`egfig8`


.. figure:: figure8.png
   :align: center
   :figclass: w



C. Build, test  and optimization
=================================

D. Validation
=============


E. Release and deploy
=====================

F. Docummentation
=================




o present the study results, we first provide an overview
of case description. Next, the research question is answered.

The text files that record the transcription verbatim of
meetings, meeting notes, as well as experience notes were
imported into NVivo (a qualitative data analysis software) [24].
We identified critical success factors from those materials
by performing inductive coding [25]. Inductive coding is an
thematic analysis technique. It uses a iterative approach to
extract data from sources and then build the common themes
to classify them. Our inductive coding process was performed
in three steps, as sho



We studied several industrial experience reports conducted
in software engineering field. We conducted our study in three
stages: (1) a study plan, (2) data collection, (3) data analysis.
Each stage is described in the following sub-sections.

Figure 3 presents an overview of the ML development lifecycle
under our CI system. Like the development of regular software, the
entire lifecycle consists of four stages (akin to a GitHub or Azure
DevOps kind of development scenario):
• Develop – the developer writes code for featurizing data, selecting an appropriate algorithm with efficient implementation, as well as basic parameter tuning; the entire ML-related
software artifact produced by this stage (including the feature extraction code) is what we refer to as a model.
• Build – the developer requests merging the code into the
master branch (a.k.a., a pull request); this automatically triggers the build process of the codebase, which trains the new
model over the training data.
• Test – the test phase follows if the build process succeeds; the
final model returned is evualuated against the test dataset,
after which the test accuracy is reported to the developer.
• Release – if all test cases are passed and the developer is
satisfied with the test accuracy, the model can then be promoted to a release environment for upstream consumption,
potentially replacing an old model that was already released.

Twelve hundred years ago  |---| in a galaxy just across the hill...

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum sapien
tortor, bibendum et pretium molestie, dapibus ac ante. Nam odio orci, interdum
sit amet placerat non, molestie sed dui. Pellentesque eu quam ac mauris
tristique sodales. Fusce sodales laoreet nulla, id pellentesque risus convallis
eget. Nam id ante gravida justo eleifend semper vel ut nisi. Phasellus
adipiscing risus quis dui facilisis fermentum. Duis quis sodales neque. Aliquam
ut tellus dolor. Etiam ac elit nec risus lobortis tempus id nec erat. Morbi eu
purus enim. Integer et velit vitae arcu interdum aliquet at eget purus. Integer
quis nisi neque. Morbi ac odio et leo dignissim sodales. Pellentesque nec nibh
nulla. Donec faucibus purus leo. Nullam vel lorem eget enim blandit ultrices.
Ut urna lacus, scelerisque nec pellentesque quis, laoreet eu magna. Quisque ac
justo vitae odio tincidunt tempus at vitae tortor.

Of course, no paper would be complete without some source code.  Without
highlighting, it would look like this::

   def sum(a, b):
       """Sum two numbers."""

       return a + b

With code-highlighting:

.. code-block:: python

   def sum(a, b):
       """Sum two numbers."""

       return a + b

Maybe also in another language, and with line numbers:

.. code-block:: c
   :linenos:

   int main() {
       for (int i = 0; i < 10; i++) {
           /* do something */
       }
       return 0;
   }

Or a snippet from the above code, starting at the correct line number:

.. code-block:: c
   :linenos:
   :linenostart: 2

   for (int i = 0; i < 10; i++) {
       /* do something */
   }
   
Inline code looks like this: :code:`chunk of code`.

Important Part
--------------

It is well known [Atr03]_ that Spice grows on the planet Dune.  Test
some maths, for example :math:`e^{\pi i} + 3 \delta`.  Or maybe an
equation on a separate line:

.. math::

   g(x) = \int_0^\infty f(x) dx

or on multiple, aligned lines:

.. math::
   :type: eqnarray

   g(x) &=& \int_0^\infty f(x) dx \\
        &=& \ldots

The area of a circle and volume of a sphere are given as

.. math::
   :label: circarea

   A(r) = \pi r^2.

.. math::
   :label: spherevol

   V(r) = \frac{4}{3} \pi r^3

We can then refer back to Equation (:ref:`circarea`) or
(:ref:`spherevol`) later.

Mauris purus enim, volutpat non dapibus et, gravida sit amet sapien. In at
consectetur lacus. Praesent orci nulla, blandit eu egestas nec, facilisis vel
lacus. Fusce non ante vitae justo faucibus facilisis. Nam venenatis lacinia
turpis. Donec eu ultrices mauris. Ut pulvinar viverra rhoncus. Vivamus
adipiscing faucibus ligula, in porta orci vehicula in. Suspendisse quis augue
arcu, sit amet accumsan diam. Vestibulum lacinia luctus dui. Aliquam odio arcu,
faucibus non laoreet ac, condimentum eu quam. Quisque et nunc non diam
consequat iaculis ut quis leo. Integer suscipit accumsan ligula. Sed nec eros a
orci aliquam dictum sed ac felis. Suspendisse sit amet dui ut ligula iaculis
sollicitudin vel id velit. Pellentesque hendrerit sapien ac ante facilisis
lacinia. Nunc sit amet sem sem. In tellus metus, elementum vitae tincidunt ac,
volutpat sit amet mauris. Maecenas [#]_ diam turpis, placerat [#]_ at adipiscing ac,
pulvinar id metus.

.. [#] On the one hand, a footnote.
.. [#] On the other hand, another footnote.

.. figure:: figure1.png

   This is the caption.:code:`chunk of code` inside of it. :label:`egfig` 

.. figure:: figure1.png
   :align: center
   :figclass: w

   This is a wide figure, specified by adding "w" to the figclass.  It is also
   center aligned, by setting the align keyword (can be left, right or center).
   This caption also has :code:`chunk of code`.

.. figure:: figure1.png
   :scale: 20%
   :figclass: bht

   This is the caption on a smaller figure that will be placed by default at the
   bottom of the page, and failing that it will be placed inline or at the top.
   Note that for now, scale is relative to a completely arbitrary original
   reference size which might be the original size of your image - you probably
   have to play with it.  :label:`egfig2`

As you can see in Figures :ref:`egfig` and :ref:`egfig2`, this is how you reference auto-numbered
figures.

.. table:: This is the caption for the materials table. :label:`mtable`

   +------------+----------------+
   | Material   | Units          |
   +============+================+
   | Stone      | 3              |
   +------------+----------------+
   | Water      | 12             |
   +------------+----------------+
   | Cement     | :math:`\alpha` |
   +------------+----------------+


We show the different quantities of materials required in Table
:ref:`mtable`.


.. The statement below shows how to adjust the width of a table.

.. raw:: latex

   \setlength{\tablewidth}{0.8\linewidth}


.. table:: This is the caption for the wide table.
   :class: w

   +--------+----+------+------+------+------+--------+
   | This   | is |  a   | very | very | wide | table  |
   +--------+----+------+------+------+------+--------+

Unfortunately, restructuredtext can be picky about tables, so if it simply
won't work try raw LaTeX:


.. raw:: latex

   \begin{table*}

     \begin{longtable*}{|l|r|r|r|}
     \hline
     \multirow{2}{*}{Projection} & \multicolumn{3}{c|}{Area in square miles}\tabularnewline
     \cline{2-4}
      & Large Horizontal Area & Large Vertical Area & Smaller Square Area\tabularnewline
     \hline
     Albers Equal Area  & 7,498.7 & 10,847.3 & 35.8\tabularnewline
     \hline
     Web Mercator & 13,410.0 & 18,271.4 & 63.0\tabularnewline
     \hline
     Difference & 5,911.3 & 7,424.1 & 27.2\tabularnewline
     \hline
     Percent Difference & 44\% & 41\% & 43\%\tabularnewline
     \hline
     \end{longtable*}

     \caption{Area Comparisons \DUrole{label}{quanitities-table}}

   \end{table*}

Perhaps we want to end off with a quote by Lao Tse [#]_:

  *Muddy water, let stand, becomes clear.*

.. [#] :math:`\mathrm{e^{-i\pi}}`

.. Customised LaTeX packages
.. -------------------------

.. Please avoid using this feature, unless agreed upon with the
.. proceedings editors.

.. ::

..   .. latex::
..      :usepackage: somepackage

..      Some custom LaTeX source here.

References
----------
.. [Atr03] P. Atreides. *How to catch a sandworm*,
           Transactions on Terraforming, 21(3):261-300, August 2003.


