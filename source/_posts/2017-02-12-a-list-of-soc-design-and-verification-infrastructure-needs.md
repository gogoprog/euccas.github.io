---
layout: post
title: "A list of SoC Design and Verification Infrastructure Needs -  Tools/Automation Flows (2013)"
date: 2017-02-12 15:53:19 -0800
comments: true
categories: Infrastructure Verification
keywords: SoC Design Verification Infrastructure Tools 
description: SoC Design and Verification Infrastructure and Tools Overview
---

*This post was written in 2013, when I thought it was necessary to summarize infrastructure tools and flows needed in SoC design and verification, according to all my experience. Today when I checked on my old notes I found this one and would like to share it here. Later on I'll update and expand this list according to my latest experience and knowledge in engineering tools and infrastructure for software and hardware development.*

System-on-Chip design and verification process is a complicated one. Unlike the world of Web and Internet, the design and development of hardware products have higher risk and lower tolerance to any mistakes. SoC design and verification process requires collaborations from multiple teams and vendors. Lots of hard decisions to make. Lots of trade-offs to consider. Moreover, the nonrecurring-engineering (NRE) charge makes sufficient and solid verification a must with limited time and resource. Tools and automated flows are an essential part of any design house.
 
Here is a list of areas that need tools and flows for SoC software and hardware design and verification according to my experience.

<table>
<tr>
	<th>Usage Area of Tools/Flows</th>
	<th>Software</th>
	<th>Hardware</th>
	<th>Design Usage</th>
	<th>Verification Usage</th>
</tr>

<tr>
	<td>Test Generation</td>
	<td>x</td>
	<td>x</td>
	<td></td>
	<td>x</td>
</tr>

<tr>
	<td>Regression System</td>
	<td>x</td>
	<td>x</td>
	<td></td>
	<td>x</td>
</tr>

<tr>
	<td>Coverage Reporting</td>
	<td>x</td>
	<td>x</td>
	<td></td>
	<td>x</td>
</tr>

<tr>
	<td>Coding Style Check</td>
	<td>x</td>
	<td>x</td>
	<td>x</td>
	<td></td>
</tr>

<tr>
	<td>Code Review System</td>
	<td>x</td>
	<td>x</td>
	<td>x</td>
	<td></td>
</tr>

<tr>
	<td>Code Quality Analysis</td>
	<td>x</td>
	<td>x</td>
	<td>x</td>
	<td></td>
</tr>

<tr>
	<td>Build System</td>
	<td>x</td>
	<td>x</td>
	<td>x</td>
	<td>x</td>
</tr>

<tr>
	<td>Version Control</td>
	<td>x</td>
	<td>x</td>
	<td>x</td>
	<td>x</td>
</tr>

<tr>
	<td>Integration System</td>
	<td>x</td>
	<td>x</td>
	<td>x</td>
	<td></td>
</tr>

<tr>
	<td>Spec System</td>
	<td></td>
	<td>x</td>
	<td>x</td>
	<td></td>
</tr>

<tr>
	<td>RTL Generation</td>
	<td></td>
	<td>x</td>
	<td>x</td>
	<td></td>
</tr>

<tr>
	<td>TestBench Generation</td>
	<td></td>
	<td>x</td>
	<td></td>
	<td>x</td>
</tr>

<tr>
	<td>Synthesis</td>
	<td></td>
	<td>x</td>
	<td>x</td>
	<td></td>
</tr>

<tr>
	<td>Netlist Quality Analysis</td>
	<td></td>
	<td>x</td>
	<td>x</td>
	<td></td>
</tr>

<tr>
	<td>Power Analysis and Optimization</td>
	<td></td>
	<td>x</td>
	<td>x</td>
	<td></td>
</tr>

<tr>
	<td>ECO Flow</td>
	<td></td>
	<td>x</td>
	<td>x</td>
	<td></td>
</tr>

<tr>
	<td>Issue/Bug Tracking System</td>
	<td>x</td>
	<td>x</td>
	<td>x</td>
	<td>x</td>
</tr>

<tr>
	<td>Infrastructure: Linux/Windows machines, LSF</td>
	<td>x</td>
	<td>x</td>
	<td>x</td>
	<td>x</td>
</tr>

</table>



