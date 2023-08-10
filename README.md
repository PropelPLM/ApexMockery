# ApexMockery

Mocking framework for Apex

## Quick start

To effectively mock and hence abstract the complexities of an object, use `ApexMockery` to inject the generated mock as a dependency of the class to be tested.

Example:
`SeriousBusiness.cls` (class to test)

```apex
public SeriousBusiness {
  public MockMe integralBusinessLogicClass;

  public void printMoney() {
    integralBusinessLogicClass.makeMoney();
   }
}
```

`SeriousBusinessTest.cls` (test class)

```apex
public SeriousBusinessTest {
  static void testPrintMoney() {
      MockProvider mock = new MockProvider(MockMe.class);
      SeriousBusiness rlySrsBiz = new SeriousBusiness();
      rlySrsBiz.integralBusinessLogicClass = (MockMe) mock.mockInstance;

      rlySrsBiz.printMoney();
      System.assert(mock.hasBeenCalled('makeMoney'), 'makeMoney should have been called');
  }
}
```
