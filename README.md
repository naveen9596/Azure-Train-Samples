# Azure-Overview

Overview of Azure Services:
============================
This file contains text you can copy and paste for the examples in Cloud Academy's Overview of Azure Services course.

Introduction:
=============
Azure Free Trial

Using the Azure Portal:
=========================
Azure Portal

Using the Azure CLI:
====================
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
cd html-docs-hello-world
az webapp up --location westus --name [your_name] --html
http://[your_name].azurewebsites.net
az group delete --name [resource_group_name]

az group list --query "[].{resource_group:name, location:location}"
az webapp up -g [resource_group] --location [location] -n [app_name] --sku S1 --html

Service Categories:
==================
Azure Products

Designing a Solution:
======================
Azure Architecture Center

Summary:
=========
Azure documentation
