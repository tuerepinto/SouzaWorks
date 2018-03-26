# SouzaWorks
This project contais a complete solution or a architecture of reference to customize CRM 365 in all levels like UI, plugins, custom workflow activities
and custom web pages and apps.

Layers
1. Crm.Model
This layer is itended to contain CRM Early bound class and any other model class to use for web api services.
Important topics about this layer:
	1.1 - To genereate CRM early bound class here you need:
		- Intall extension from https://github.com/xairrick/CrmCodeGenerator in your VS.
		- Rigth mouse click on CrmEntityes.tt and select menu item "Run Custom Tool"
		- After conect to you organization and inform entities you want on the project, the class CrmEntities.cs will be update.

2. CRM.Console.Carga
 This is a console app to run any eventualy task at any time like load some data, bulk update to fit some businnes change, etc.
 To use this simple code your task on main class, then change to connection settings on appSettings.config to use a test organization.
 After everyting is fine change appSettings.config to user production organization and run your program.
 Note: Befone program any task here you shold think if it cold be done by a temporary worflow. 
 For example update a fied with a constant value cold be done by workflow executed on selectd records. 

3. Crm.Dominio
This layer is intended to contain all bussinees class with you need to extend crm. 
This is a core layer, so you should use this as a reference in projects like AzureWebJobs, Console Apps, Web Api or Web App where you need 
some type of custom interaction with CRM SDK. In project CRM.Console.Carga we demostrate this.

4. Crm.Reposotorio
This layer is intended to contain CRM Data Access using SDK Api. Here we add a Context class to connect to CRM API and some
helpfull class with metods to interact with api. Once again this is a core layer and intend to be referened only by Domain Layer. 


4. Crm.Plugins
This layer implement custom plugins to do any custom task or validation on your CRM. This project is ok to register on CRM. 
We alread have done all needed references and signed the assembly as required to register plugins library.
Remember to do not introduce others custom dlls dependences here because CRM suport register only a single assembly.
Notes: 
 - For simplify code job here we use only late bound entity.
 - Register CRMArchitecture_1_0_0_0 if you want se tests I have made on CRM.Forms.js and AutoNumber.cs plugin. This solution create a entity
 named FormTest wher you should create a register and chose a value on function field to test a function.
 This soluction also create a AutoNumber entity where you should create a record with respectively values:
	  Nome=Number to Orders
	  Target Entity Name=crmarch_order
	  Target Field=crmarch_order_number
	  Current Number=0
	  Prefixo=Order
	  Sufixo=ZZ
  After that simple create some records in Order entity to se autonumber in action.
  
5. Crm.WorkFlows
As in Plugin Layer this layer is read to register custom activities on your CRM. 
All plugins notes and recomendations is aplied here.
Your should code you custom activities here folowing samples we have done.

6. Crm.UIExtension
This Layer is intend to contain any code created to customize crm forms. 
As a good practice you should first code or change your script here is this layer to be versioned in your source control and then upload to CRM as a web resorce.
Notes:
 - CRM.Form.js: This java script file is intended to contain any code with could be reused in forms. So code any util function here e add a reference in your form.
 - Entities/Account.js: This script is a sample how to customize a entity form. Here we have samples to form onload and onsave event plus a field change.
 - This layer is configured on solution to do not compile.
 
 7.Crm.WebExtension
 Use this web site to develop custom api services to invoke from crm forms when you need. 
 For example if you need complete a form with address base in a zipcode field. To do this your need invoke a service to retrieve a address.
 In some cenarios you could need a iframe to display some extra information. Use this site to acomplish this creating a razor view.

 Note: In CRM.Forms.js you should create a function to invoke a custom api method using like the GetAddress operation here.
