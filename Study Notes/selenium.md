

JavascriptExecutor js = (JavaScriptExecutor) driver;
js.executeScript...

actions.dragAndDrop(element, toElement)

# Actions


```java
Actions action = new Actions(driver);
action.moveToElement(passwordField);
```

field.sendKeys(Keys.ENTER);

## File upload

```java
fileUploadElement.sendKeys("pathOfTheFile);
```

## Waits

### Implicit waits

```java
driver.manage().timeouts().implicitlyWait(5, TimeUnit.SECONDS);
```

### Explicit waits

```java
WebDriverWait wait = new WebDriverWait(driver, 10);
```


## Selenium Grid

> java -jar selenium-server-standalone-3.141.59.jar -role hub


## Cloud testing solutions

* SauceLabs


---


// newGroupInput.getAttribute("value")
