# Appium
# swip or scroll

package Deemo;

import java.net.MalformedURLException;
import java.net.URI;
import java.net.URL;
import java.time.Duration;
import java.util.Collections;

import org.openqa.selenium.By;
import org.openqa.selenium.Dimension;
import org.openqa.selenium.interactions.Pause;
import org.openqa.selenium.interactions.PointerInput;
import org.openqa.selenium.interactions.Sequence;
import org.openqa.selenium.remote.DesiredCapabilities;

import io.appium.java_client.android.AndroidDriver;

public class SwiporScroll {

	public static void main(String[] args) throws MalformedURLException, InterruptedException {
		// TODO Auto-generated method stub
		DesiredCapabilities capabilities = new DesiredCapabilities();
		capabilities.setCapability("platformName", "Android");
		capabilities.setCapability("appium:platformVersion", "11");
		capabilities.setCapability("appium:deviceName", "Samsung SMA207F");
		capabilities.setCapability("appium:automationName", "uiautomator2");
		capabilities.setCapability("appium:appPackage","io.appium.android.apis");
		capabilities.setCapability("appium:appActivity","io.appium.android.apis.ApiDemos");
		
		URL url = URI.create("http://127.0.0.1:4723/").toURL();
		
		AndroidDriver driver = new AndroidDriver(url,capabilities);
		
		Thread.sleep(5000);
		System.out.println("application started");
		
		//click on view button
		driver.findElement(By.xpath("//android.widget.TextView[@content-desc=\"Views\"]")).click();
		
		//get screen size
		Dimension size = driver.manage().window().getSize();
		
		//find the position where you need to touch
		int startX = size.getWidth() / 2;
		int startY = size.getHeight() / 2;
		
		//position till you want to move your finger to swipe
		int endX = startX;
		int endY = (int) (size.getHeight() * 0.25);
		
		//pointerInput class to create a sequence of actions
		PointerInput finger1 = new PointerInput(PointerInput.Kind.TOUCH, "finger1");
		
		//sequence object, which is a list of actions that will be performed
		Sequence sequence = new Sequence(finger1, 1)
				.addAction(finger1.createPointerMove(Duration.ZERO, PointerInput.Origin.viewport(), startX, startY))
		        .addAction(finger1.createPointerDown(PointerInput.MouseButton.LEFT.asArg()))
		        .addAction(new Pause(finger1, Duration.ofMillis(200)))
		        .addAction(finger1.createPointerMove(Duration.ofMillis(100), PointerInput.Origin.viewport(), endX, endY))
		        .addAction(finger1.createPointerUp(PointerInput.MouseButton.LEFT.asArg()));
		
		//perform the sequence of action
		driver.perform(Collections.singletonList(sequence));
		
		Thread.sleep(2000);
		driver.quit();
		
		

	}

}


