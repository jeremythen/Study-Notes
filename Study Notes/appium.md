
# Appium

## driver.getPageSource() to get the source of a view
```Java
System.out.println(driver.getPageSource());
```

## Automate web browsers/ apps that display through a web browser, replace the 'app' capability with the 'browserName' capability.

```Java
caps.setCapability("browserName", "Safari");

driver = new RemoteWebDriver(new URL(THEURL), caps);
```

Now we can use:

```Java
driver.findElement(By.linkText("All Editions")) // linkText or css selectors.
```

## Waiting

```Java
WebDriverWait wait = new WebDriverWait(driver, 10);
driver.get("https://appiumpro.com);
```

## Api

TouchAction -> To handle any combination of digits and motions.



