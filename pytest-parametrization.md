# How to declare parametrizations
  > Using parametrizations we can provide multiple test data for single input methods
  > We can pass the test data in the method itself or using excel also we can provide the test data

    > in parametrizations.py files
    --------------------------------------------------
    class TestClass:
        @pytest.mark.parametrize('user,pwd',[("Admin","admin123"),("Adm","admin123"),("Admin","admin")])
        def test_Login(self,user,pwd):
            self.driver= WebDriver.Chrome()
            self.driver.get("application use")
            ............

        
  
