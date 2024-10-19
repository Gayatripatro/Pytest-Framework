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
      @pytest.fixture()  # decorator
      def setup(self):   
        print("Lunching the browser")  # Execuute once before every test method
        print("Opening the URL")        # Execuute once before every test method
        yield
        print("Closing the browser")    # Execuute once after every test method
      def test_loginwithvalidcredentials(self,setup):
        print("Login successfully")
      def loginwithwrongcredentials(self):
        print("Please enter correct credentials")


# Run Commands:
#### For running a particular Module:
> **pytest -v -s Filename\module name**

> EX : pytest -v -s algoQATCs\test_login.py


#### For running a
