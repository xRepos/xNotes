---
title: Informaztion Value(IV)
description: The calculation of Weight of evidence(WOE) and Information Value(IV)
--- 

Information Value
=================

Calculation of Weight of Evidence(WOE)
--------------------------------------

Weight of evidence(WOE):

$$ WOE_i=\log({\verb+% pos+_i \over \verb+% neg+_i})$$

where $$ i=1,2, ... k$$, and $$k$$ is the number of bins.

Calculation of Information Value(IV)
------------------------------------

Information Value(IV):

$$ IV = \sum_{i=1}^k \{(\verb+% pos+_i - \verb+% neg+_i) \times WOE_i \}$$