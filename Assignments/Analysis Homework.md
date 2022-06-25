# Analysis of an Open Source Project
For this project I will be analyzing Tensorflow, NumPy, and HyperNerf followed by a more in depth written analysis on NumPy.
## Part 1: Tables based on the foss2serve [rubric](http://foss2serve.org/index.php/Project_Evaluation_Rubric_(Activity))
### [TensorFlow](https://github.com/tensorflow/tensorflow)
Tensorflow is a google project that has become one of the largest open source machine learning libraries along side pytorch.
| #   | Evaluation Factor      | Level <br /> (0-2) |                                                                             Evaluation Data                                                                              |
| --- | :--------------------- | :----------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| 1   | Licensing              |         2          |                                                                            Apache-2.0 license                                                                            |
| 2   | Language               |         2          |                                                                   C++: 62.7% Python: 22.2% MLIR: 5.3%                                                                    |
| 3   | Level of Activity      |         2          |                                                            Active the whole year with >180 commits every week                                                            |
| 4   | Number of Contributors |         2          |                                                                            3,129 contributors                                                                            |
| 5   | Product Size           |         1          |                                                        Massive with a 900.84 MB repo and about 6.5m lines of code                                                        |
| 6   | Issue Tracker          |         2          |                                                 Open: 2,101 Closed: 32,867  Good First Issues: 233 Overall: Very Active                                                  |
| 7   | New Contributor        |         2          | [Great introduction](https://github.com/tensorflow/tensorflow/blob/master/CONTRIBUTING.md) with in depth contribution guidelines and documentation <br /> High standards |
| 8   | Community Norms        |         2          |                                   [Detailed code of conduct](https://github.com/tensorflow/tensorflow/blob/master/CODE_OF_CONDUCT.md)                                    |
| 9   | User Base              |         2          |         Massive user base as Tensorflow is one of the leading tools for ML development <br /> Bindings in many different languages <br /> Used by 200k on GitHub with 166k stars         |
|     | **Total Score**        |         17         |

Explanation:
1. Licensing
2. Language
3. Level of Activity
4. Number of Contributors
5. Product Size
6. Issue Tracker
7. New Contributor
8. Community Norms
9. User Base
### [NumPy](https://github.com/numpy/numpy)
NumPy is an extremely popular python package for scientific computing and is essential to most higher level math functions in python.
| #   | Evaluation Factor      | Level <br /> (0-2) |                                                             Evaluation Data                                                             |
| --- | :--------------------- | :----------------: | :-------------------------------------------------------------------------------------------------------------------------------------: |
| 1   | Licensing              |         2          |                                                 BSD 3-Clause "New" or "Revised" License                                                 |
| 2   | Language               |         2          |                                                    Python: 62.4% C: 35.2% C++: 1.2%                                                     |
| 3   | Level of Activity      |         2          |                                            Active the whole year with >10 commits every week                                            |
| 4   | Number of Contributors |         2          |                                                                  1,330                                                                  |
| 5   | Product Size           |         1          |                                            Large at 108.41 MB and about 277.5k lines of code                                            |
| 6   | Issue Tracker          |         2          |                                 Open: 1,990 Closed: 8,689  Good First Issues: N/A Overall: Very Active                                  |
| 7   | New Contributor        |         2          | [Clear guidelines](https://numpy.org/devdocs/dev/index.html) and great documentation <br /> However no clearly marked good first issues |
| 8   | Community Norms        |         2          |                [Detailed code of conduct](https://numpy.org/code-of-conduct/) that is well organized on an external site                |
| 9   | User Base              |         2          |       Massive user base <br /> One of the most popular python libraries, easily installed with pip <br /> Used by 1.1m on GitHub with 20.8k stars       |
|     | **Total Score**        |         17         |

### [HyperNerf](https://github.com/google/hypernerf) 
HyperNerf is relatively new research project in novel view synthesis by google.
| #   | Evaluation Factor      | Level <br /> (0-2) |                                                             Evaluation Data                                                             |
| --- | :--------------------- | :----------------: | :-------------------------------------------------------------------------------------------------------------------------------------: |
| 1   | Licensing              |         2          |Apache-2.0 license|
| 2   | Language               |         2          |Python: 52.2% Jupter Notebook: 47.8%|
| 3   | Level of Activity      |         1          |One quarter active with inconsistent commits|
| 4   | Number of Contributors |         1          |3|
| 5   | Product Size           |         1          |Small at 154 KB and around 13k lines of code|
| 6   | Issue Tracker          |         1          |Open: 15 Closed: 6 Good First ISsues: None Overall: barely active|
| 7   | New Contributor        |         1          | [Very short introduction](https://github.com/google/hypernerf/blob/main/CONTRIBUTING.md) does not establish clear standards <br /> does not point to a good place to start|
| 8   | Community Norms        |         2          |  [Great code of conduct included](https://opensource.google/conduct/) that comes with all google open source projects         |
| 9   | User Base              |         1          |Small user base with 595 stars on github and mostly researcher interest|
|     | **Total Score**        |         12         |

## Part 2: In Depth Analysis of NumPy

NumPY is an easy to use numerical computing library for python that offers high speed performance with an extensive feature set. NumPY was founded by data scientist [Travis Oliphant in 2005](https://scipy.github.io/old-wiki/pages/History_of_SciPy) who wanted to bring unity into the python based scientific computing community and the project quickly grew to be included in millions of projects around the world largely thanks to Oliphant's dedication to open sourcing the project. NumPy allows users to easily manipulate high dimensional data, compute various linear algebra operations, perform essential data science operations, sort data, and more. Soon an entire charity named [NumFocus](https://numfocus.org/project/numpy) was built to financially support fully open source projects like NumPY and the library's mass adoption even made it a candidate to be included into the base version of python, however this never materialized. 

