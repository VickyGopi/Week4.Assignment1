package week4.day1;

import java.util.concurrent.TimeUnit;

import org.apache.commons.io.FileUtils;
import org.openqa.selenium.By;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import java.io.File;
import java.io.IOException;

import io.github.bonigarcia.wdm.WebDriverManager;

public class Assignment1 {

	public static void main(String[] args) throws IOException {
		WebDriverManager.chromedriver().setup();
		ChromeDriver driver = new ChromeDriver();
		driver.get("https://jqueryui.com/sortable/");
		driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
		driver.manage().window().maximize();
		WebElement Frame = driver.findElement(By.className("demo-frame"));
		driver.switchTo().frame(Frame);
		WebElement Item1 = driver.findElement(By.xpath("//li[text()='Item 1']"));
		WebElement Item4 = driver.findElement(By.xpath("//li[text()='Item 4']"));
		System.out.println(Item4.getLocation().getX());
		System.out.println(Item4.getLocation().getY());
		Actions Build = new Actions(driver);
		Build.dragAndDropBy(Item1, Item4.getLocation().getX(), Item4.getLocation().getY()).perform();
		File source = driver.getScreenshotAs(OutputType.FILE);
		File target = new File ("./snaps/sortable.png");
		FileUtils.copyFile(source, target);
		driver.switchTo().defaultContent();
		driver.close();
	}
}
