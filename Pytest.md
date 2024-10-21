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
> Inside **conftest.py** only you have to write the setup methods so that from anywhere in your project you can access those data

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

#### For execute test cases in a group
> pytest -v -s -m "Regression" algoQATcs\test_Grouping.py
        
> pytest -v -s -m "Regression and Sanity" algoQATcs\test_Grouping.py

> pytest -v -s -m "not Regression" algoQATcs\test_Grouping.py   # it will execute only sanity Tcs


#### For running test cases parallel
> pytest -n=3 -v -s algoQATcs\test_parallel.py



# Benifit of using pytest
. we can skip the test cases (If you want to skip any test cases/methods before that method you need to use **"@pytest.mark.skip"** then it will not execute)

. we can order the test cases (Which sequence you need to execute your test cases accordingly u need to update as **"@pytest.mark.forst" or "@pytest.mark.second" and all**)
      > For ordering you need to create a file with the name as **"pytest.ini"** in that you need to update all the customized markers so that pytest will identify it easily while execution
      > Need to install **"pytest-ordering"** package for ordering test cases execute 
      > or u can use **"@pytest.mark.run(order=1)"** like this
      
      > in pytest.ini file
      -------------------------------------------
      [pytest]
      markers=
            first
            second
            third
            fourth
            dependency
            Sanity
            Regression

. we can mention dependent test cases : (If our test cases depend on any other test cases and if that test case fails then we should skip the dependent test cases so that it will save our time)
      > **"@pytest.mark.dependency(depends=['clssname::test_methods'])"**
      > or **"@pytest.mark.dependency(depends=['clssname::test_methods1','clssname::test_methods2'])"**
      > If there is multiple dependency methods are there then if 1 test cases also failed means the dependent test cases will be Skipped
      > need to add **"dependency"** keyword in the pytest.ini file

      > in test_depedency.py file
      ------------------------------------
      import pytest
      class TestLogin:
            @pytest.mark.dependency()
            def test_openApp(self):
                  assert False
                  
            @pytest.mark.dependency('depends=['TestLogin::test_openApp')
            def test_login(self):
                  assert True
                  
            @pytest.mark.dependency('depends=['TestLogin::test_openApp','TestLogin::test_login')
            def test_search(self):
                  assert True
             
              

. Grouping testing : ( We can group our test cases as Sanity, regression or both sanity and regression and all so that according to our requirement we can execute the test cases)
      > **"@pytest.mark.Sanity"** 
      > **"@pytest.mark.Regression"** 

      > ** Execution Details**
            pytest -v -s -m "Regression" algoQATcs\test_Grouping.py            
            pytest -v -s -m "Regression and Sanity" algoQATcs\test_Grouping.py
            pytest -v -s -m "not Regression" algoQATcs\test_Grouping.py   # it will execute only sanity Tcs




      > in test_Grouping.py file
      ------------------------------------
      import pytest
      class TestLogin:
            @pytest.mark.Sanity
            def test_openApp(self):
                  assert False
                  
            @pytest.mark.Regression
            def test_login(self):
                  assert True
                  
            @pytest.mark.Sanity
            @pytest.mark.Regression
            def test_search(self):
                  assert True
      

      
      
      

. Parallel test cases execution :
      > need to install package : **pytest-xdist**
      
      > pytest -n=3 -v -s algoQATcs\test_parallel.py

