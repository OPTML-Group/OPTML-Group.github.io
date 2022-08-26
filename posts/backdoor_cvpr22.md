---
title: "Quarantine: Sparsity Can Uncover the Trojan Attack Trigger for Free"
date: 2022-06-22
author: Yihua Zhang
layout: post
sitemap: false
---

## How does the model sparsity relate to its train-time robustness against Trojan attacks?

![Research Achievements At-A-Glance]({{ site.url }}{{ site.baseurl }}/images/postpic/backdoor_cvpr22/overview.png){: style="width: 60%; float: middle"}

* Trojan features learned by backdoored attacks are significantly more stable against pruning than benign features. Therefore, Trojan attacks can be uncovered through the pruning dynamics of the Trojan model. 

* Leveraging LTH-oriented iterative magnitude pruning (IMP), the ‘winning Trojan Ticket’ can be discovered, which preserves the Trojan attack performance while retaining chance-level performance on clean inputs. 

* The winning Trojan ticket can be detected by our proposed linear model connectivity (LMC)-based Trojan score.


