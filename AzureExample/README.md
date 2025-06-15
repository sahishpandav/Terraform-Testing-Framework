# Terraform-Testing-Framework

Terraform Test (TerraTest)

This testing framework is available in Terraform v1.6.0 and later. 
This framework allows you to write unit tests for your terraform modules.

IaC testing is a little bit different from Software Testing. Terraform doesn't have methods or functions for you to unit test. The methods or functions in the terraform is baked into the binary, not something that you are responsible for testing, e.g. regex(), lower(), etc
If not functions then what is supposed to be tested in terraform code: 
Basic validity: Is my code valid? 
Basic syntax and parse logic. Terraform(HCL) isn’t a compiled language. So we are not testing if the code compiles, we are testing for terraform at the core engine should be able to parse it properly, using plugins and providers. A specified argument in each resource actually exists or that you’ve supplied the right data type for that argument. 
terraform validate - checks if the code is syntactically correct. 
Unit Testing: 
Then there is testing to make sure that the configuration renders the way you expect based on the given input. For this you have to add conditional logic or function or validation in your code.  Suppose if you receive some bad input from the end-user in your terraform configuration it should be handled correctly.
Integration Testing: 
Checking if the deployed infrastructure works as expected. Verifying the resources are correctly deployed or not.

Terraform Test Framework: 
Terraform test framework is introduced to answer the later two questions - unit testing and integration testing. 
For this previously we need to use third party tools like terratest(go lang) or kitchen terraform(ruby). 
Terraform test is a way to declaratively express a series of tests to run against a given configuration. Framework uses hcl like terraform. 
Each test that you are going to define uses a run action for running the test. 
run “test1” {}
run “test2” {}
run “test3” {}
And that executes either a terraform plan or a terraform apply. To verify the functionality of the configuration each run that you have can have one or more assertion that checks a condition and logs the result. If all the assertions in a run pass, the test passes. If any of the assertions in a test fails then the test fails. 
assert{
	condition = true | false
	error = “message”
}
You can specify additional information for each test run - things you want to test for 
Like input variables values
variables{
	instances = 20
	account = “Standard”
}
To see what the runs look like if I specify these input variables. You can also define provider configuration per test or for the entire test. You can also supply mock data for certain resources. 

