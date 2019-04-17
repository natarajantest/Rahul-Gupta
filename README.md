# Rahul-Gupta
//=======Hospital App================
package initialize;

import java.time.Duration;
import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.WebDriverWait;

public class OpenEMR {

	public static void main(String[] args) throws InterruptedException {
		WebDriver driver = new ChromeDriver();
		WebDriverWait wait = new WebDriverWait(driver,30);
		driver.manage().window().maximize();
		driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
		driver.get("https://demo.openemr.io/d/openemr");
		driver.findElement(By.id("authUser")).sendKeys("admin");
		driver.findElement(By.id("clearPass")).sendKeys("pass");
		driver.findElement(By.xpath("//button[@class='btn btn-default btn-lg']")).click();
		driver.findElement(By.xpath("//div[@class='menuSection']")).click();
		Actions act  = new Actions(driver);
		act.moveToElement(driver.findElement(By.xpath("//div[text()='Patient/Client']"))).build().perform();
		 act
			.keyDown(Keys.CONTROL)
			.pause(Duration.ofSeconds(1))
			.build()
			.perform();
		driver.findElement(By.xpath("//div[text()='New/Search']")).click();
		
		driver.switchTo().frame(driver.findElement(By.name("pat")));
		
		driver.findElement(By.id("form_fname")).sendKeys("Rahul");
		driver.findElement(By.id("form_lname")).sendKeys("Gupta");
		driver.findElement(By.id("form_DOB")).sendKeys("2019-04-17");
		driver.findElement(By.id("form_sex")).sendKeys("Male");
		driver.findElement(By.id("form_fname")).sendKeys("Rahul");

		driver.findElement(By.id("create")).click();
		driver.switchTo().defaultContent();
		driver.switchTo().frame(driver.findElement(By.id("modalframe")));
		
		driver.findElement(By.xpath("//input[@value='Confirm Create New Patient']")).click();
		Thread.sleep(5000);
		driver.switchTo().alert().accept();
		driver.findElement(By.className("closeDlgIframe")).click();
		act.moveToElement(driver.findElement(By.xpath("//div[@class='menuSection userSection']"))).build().perform();
	    driver.findElement(By.xpath("//ul//li[text()='Logout']")).click();		
	}

}
