#### Project Name ----> Directory ------> Modules/Files(.py) ----> Class ----> Test methods
#### EX : alogoQAFunctionlTCs ----> algoQATCs --> test_login.py ----> TestLogin ----> withValidCredentials_test

# Naming conventions:
1. The Files name should start with **"test_"** or end with **"_test"** (EX: **test_login.py** or **login_test.py**)
2. Class name should start with **"Test"** (EX: **TestLogin**)
3. Test method should start with **"test_"** (Ex: **login_test**)


# Fixture:
> When you create a fixture method when ever you will call that method that time it will execute before the test cases are executed. If you did not pass the fixture method name for any test cases that time it will not execute for that particular test cases.
> 
> Even if you want to execute some code after the test cases are executed also you can mention in the same fixture method using **yield** (So before yield method whatever it will be there will execute before the test cases are executed and after the yield whatever you mentioned it will execute after the test cases executed)
>
> Inside **conftest.py** only you have to write the setup methods so that from any where of your project you can access those data

> EX:
> 
      inside conftest.py file
      ---------------------------------------------------------------
      import pytest
      @pytest.fixture()  # decorator
      def setup():   
        print("Lunching the browser")  # Execuute once before every test method
        print("Opening the URL")        # Execuute once before every test method
        yield
        print("Closing the browser")    # Execuute once after every test method

      inside test_login.py files
      ----------------------------------------------------------------------
      import pytest
      Class TestLogin:
            def test_loginWithValidCredentials(self,setup):
                  print("Login successfully")
            def loginwithwrongcredentials(self):
                  print("Please enter correct credentials")


# Run Commands:
#### For running a particular Module:
> **pytest -v -s Filename\module name**

> EX : pytest -v -s algoQATCs\test_login.py


#### For running a single module:
> **pytest -v -s Filename\modules\module name.py**

> EX : pytest -v -s algoQATCs\modules\test_login.py


#### For running all the modules at a time:
> **pytest -v -s Filename\modules*

> EX : pytest -v -s algoQATCs\modules

#### For running a specific method from a module:
> **pytest -v -s Filename\modules\module name.py::class name::methodname**

> EX : pytest -v -s algoQATCs\modules\test_login.py::TestLogin::test_loginWithValidCredentials

.

# Benifit of using pytest
. we can skip the test cases (If you want to skip any test cases/methods before that method you need to use **"@pytest.mark.skip"** then it will not execute)

. we can order the test cases (Which sequence you need to execute your test cases accordingly u need to update as **"@pytest.mark.forst" or "@pytest.mark.second" and all**)
      > For ordering you need to create a file with the name as **"pytest.ini"** in that you need to update all the customized markers so that pytest will identify it easily while execution
      > Need to install **"pytest_ordering"** package for ordering test cases execute 
      > or u can use **"@pytest.mark.run(order=1)"** like this
      
      > in pytest.ini file
      -------------------------------------------
      [pytest]
      markers=
            first
            second
            third
            fourth

. we can mention dependent test cases : ()

. Parallel testing

. Group the test cases
