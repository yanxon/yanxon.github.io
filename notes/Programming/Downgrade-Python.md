---
layout: page
title: How to Downgrade Python Version
description:
---

Recently, I learned that TensorFlow runs only on Python 3.4, 3.5, or 3.6 for Python3 version. If you download Anaconda 5.3.1, it will install Python version 3.7. Therefore, you have to downgrade your Python version. In Windows, you can do do the following:

First, you have to check the availability of all downloadable Python versions:

```
conda search python
```

This will give you such results:
```
# Name                  Version           Build  Channel
python                    2.6.8               5  pkgs/free
python                    2.6.8               6  pkgs/free
python                    2.6.9               0  pkgs/free
python                    2.6.9               1  pkgs/free
python                    2.7.3               2  pkgs/free
python                    2.7.3               3  pkgs/free
python                    2.7.3               4  pkgs/free
python                    2.7.3               5  pkgs/free
python                    2.7.3               6  pkgs/free
python                    2.7.3               7  pkgs/free
python                    2.7.4               0  pkgs/free
python                    2.7.5               0  pkgs/free
python                    2.7.5               1  pkgs/free
python                    2.7.5               2  pkgs/free
python                    2.7.6               0  pkgs/free
python                    2.7.6               2  pkgs/free
python                    2.7.7               0  pkgs/free
python                    2.7.7               1  pkgs/free
python                    2.7.7               2  pkgs/free
python                    2.7.8               0  pkgs/free
python                    2.7.9               0  pkgs/free
python                    2.7.9               1  pkgs/free
python                   2.7.10               0  pkgs/free
python                   2.7.10               1  pkgs/free
python                   2.7.10               3  pkgs/free
python                   2.7.10               4  pkgs/free
python                   2.7.10               5  pkgs/free
python                   2.7.11               0  pkgs/free
python                   2.7.11               1  pkgs/free
python                   2.7.11               2  pkgs/free
python                   2.7.11               4  pkgs/free
python                   2.7.11               5  pkgs/free
python                   2.7.12               0  pkgs/free
python                   2.7.13               0  pkgs/free
python                   2.7.13               1  pkgs/free
python                   2.7.13     h1b6d89f_16  pkgs/main
python                   2.7.13     h9912b81_15  pkgs/main
python                   2.7.13     hb034564_12  pkgs/main
python                   2.7.14     h2765ee6_18  pkgs/main
python                   2.7.14     h3e68818_15  pkgs/main
python                   2.7.14     h4084c39_22  pkgs/main
python                   2.7.14     h4a10d90_30  pkgs/main
python                   2.7.14     h4a10d90_31  pkgs/main
python                   2.7.14     h59f5a59_20  pkgs/main
python                   2.7.14     h819644d_16  pkgs/main
python                   2.7.14     h8c3f1cb_23  pkgs/main
python                   2.7.15      h2880e7c_2  pkgs/main
python                   2.7.15      h2880e7c_3  pkgs/main
python                   2.7.15      h2880e7c_4  pkgs/main
python                   2.7.15      hcb6e200_5  pkgs/main
python                   2.7.15      he216670_0  pkgs/main
python                    3.3.0               4  pkgs/free
python                    3.3.1               0  pkgs/free
python                    3.3.2               0  pkgs/free
python                    3.3.3               0  pkgs/free
python                    3.3.4               0  pkgs/free
python                    3.3.5               0  pkgs/free
python                    3.3.5               1  pkgs/free
python                    3.3.5               2  pkgs/free
python                    3.4.0               0  pkgs/free
python                    3.4.1               0  pkgs/free
python                    3.4.1               1  pkgs/free
python                    3.4.1               2  pkgs/free
python                    3.4.2               0  pkgs/free
python                    3.4.2               1  pkgs/free
python                    3.4.3               0  pkgs/free
python                    3.4.3               3  pkgs/free
python                    3.4.3               4  pkgs/free
python                    3.4.3               5  pkgs/free
python                    3.4.4               0  pkgs/free
python                    3.4.4               1  pkgs/free
python                    3.4.4               2  pkgs/free
python                    3.4.4               4  pkgs/free
python                    3.4.4               5  pkgs/free
python                    3.4.5               0  pkgs/free
python                    3.5.0               0  pkgs/free
python                    3.5.0               1  pkgs/free
python                    3.5.0               2  pkgs/free
python                    3.5.0               3  pkgs/free
python                    3.5.0               4  pkgs/free
python                    3.5.1               0  pkgs/free
python                    3.5.1               1  pkgs/free
python                    3.5.1               2  pkgs/free
python                    3.5.1               4  pkgs/free
python                    3.5.1               5  pkgs/free
python                    3.5.2               0  pkgs/free
python                    3.5.3               0  pkgs/free
python                    3.5.3               2  pkgs/free
python                    3.5.3               3  pkgs/free
python                    3.5.4               0  pkgs/free
python                    3.5.4     h1357f44_23  pkgs/main
python                    3.5.4     hc495aa9_21  pkgs/main
python                    3.5.4     hd3c4935_11  pkgs/main
python                    3.5.4     hdec4e59_20  pkgs/main
python                    3.5.4     hedc2606_15  pkgs/main
python                    3.5.5      h0c2934d_0  pkgs/main
python                    3.5.5      h0c2934d_1  pkgs/main
python                    3.5.5      h0c2934d_2  pkgs/main
python                    3.5.6      he025d50_0  pkgs/main
python                    3.6.0               0  pkgs/free
python                    3.6.1               0  pkgs/free
python                    3.6.1               2  pkgs/free
python                    3.6.2               0  pkgs/free
python                    3.6.2     h09676a0_15  pkgs/main
python                    3.6.2     h6679aeb_11  pkgs/main
python                    3.6.3      h210ce5f_2  pkgs/main
python                    3.6.3      h3389d20_0  pkgs/main
python                    3.6.3      h3b118a2_4  pkgs/main
python                    3.6.3      h9e2ca53_1  pkgs/main
python                    3.6.4      h0c2934d_2  pkgs/main
python                    3.6.4      h0c2934d_3  pkgs/main
python                    3.6.4      h6538335_0  pkgs/main
python                    3.6.4      h6538335_1  pkgs/main
python                    3.6.5      h0c2934d_0  pkgs/main
python                    3.6.6      hea74fb7_0  pkgs/main
python                    3.6.7      h33f27b4_0  pkgs/main
python                    3.6.7      h33f27b4_1  pkgs/main
python                    3.6.7      h9f7ef89_2  pkgs/main
python                    3.7.0      hea74fb7_0  pkgs/main
python                    3.7.1      h33f27b4_3  pkgs/main
python                    3.7.1      h33f27b4_4  pkgs/main
python                    3.7.1      h8c8aaf0_6  pkgs/main
python                    3.7.1      he44a216_5  pkgs/main
```

Finally, downgrading can be easily done by executing this command:

```
conda install python=3.6.7
```
