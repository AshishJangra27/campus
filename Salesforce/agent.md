# Sign Up for an Org and Install Coral Cloud App  

## 1. Sign Up for an Agentforce Enabled Developer Edition  
- Click the link below to sign up:  [Agentforce Developer Edition](https://sforce.co/workshop1)  




## 2. Install the Coral Cloud App in Your Org  

### a. Modify the URL  
- Once logged into your org, **replace** the URL segment that comes after `lightning.force.com` with:  
```/packaging/installPackage.apexp?p0=04tgL00000006DVQAY```





## 3. Configure the Coral Cloud Agent  

### **Topic Configuration**  

| Field                | Value |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Topic Label**      | Customer Experience Support |
| **Classification Description** | This topic addresses customer inquiries and issues related to booking experiences at Coral Cloud Resort, including making reservations, modifying bookings, and answering queries about experience details. |
| **Scope**           | The agent's job is to assist users in navigating and managing bookings for different experiences offered by Coral Cloud Resort, ensuring a seamless customer service experience by providing accurate information and resolving issues promptly. |
| **Instruction**     | If a customer would like more information on **Activities** or **Experiences**, you should search for the related `Experience__c` records and summarize the output. **Do not** share information about available slots, IDs, or Record Numbers. |





## 4. Verify Credit Instructions
```Can you let me know more about the full moon beach party experience?```

```Issue $100 resort credit to contact named Sofia Rodriguez```


## 5. Apex Weather Class
```
public with sharing class CheckWeather {
    @InvocableMethod(
        label='Check Weather'
        description='Check weather at Coral Cloud Resorts at a specific date. The date must be in the future, not today or earlier.'
    )
    public static List<WeatherResponse> getWeather(
        List<WeatherRequest> requests
    ) {
        // Retrieve the date for which we want to check the weather
        Datetime dateToCheck = (Datetime) requests[0].dateToCheck;

        // Call a weather service to retrieve the weather through an API call
        WeatherService.Weather weather = WeatherService.getResortWeather(
            dateToCheck
        );

        // Create the response for the agent
        WeatherResponse response = new WeatherResponse();
        response.minTemperature = weather.minTemperatureC;
        response.maxTemperature = weather.maxTemperatureC;
        response.temperatureDescription =
            'Temperatures will be between ' +
            weather.minTemperatureC +
            '°C (' +
            weather.minTemperatureF +
            '°F) and ' +
            weather.maxTemperatureC +
            '°C (' +
            weather.maxTemperatureF +
            '°F) at Coral Cloud Resorts.';
        return new List<WeatherResponse>{ response };
    }

    public class WeatherRequest {
        @InvocableVariable(
            required=true
            description='Date for which we want to check the temperature. The variable needs to be an Apex Date type with format    yyyy-MM-dd.'
        )
        public Date dateToCheck;
    }

    public class WeatherResponse {
        @InvocableVariable(
            description='Minimum temperature in Celsius at Coral Cloud Resorts location for the provided date'
        )
        public Decimal minTemperature;
        @InvocableVariable(
            description='Maximum temperature in Celsius at Coral Cloud Resorts location for the provided date'
        )
        public Decimal maxTemperature;
        @InvocableVariable(
            description='Description of temperatures at Coral Cloud Resorts location for the provided date'
        )
        public String temperatureDescription;
    }
}
```




## 6. Verify Weather Action
```Check the weather for tomorrow```


## 7. Create your own Agent
| Field                                      | Value  |
|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Topic Label**                            | Coral Cloud Service Agent |
| **Description**                            | This is the Coral Cloud Agent that helps customers learn more about Experiences as well as book sessions. |
| **Role**                                   | The agent's job is to assist users in navigating and managing bookings for different experiences offered by Coral Cloud Resorts, ensuring a seamless customer service experience by providing accurate information and resolving issues promptly. |
| **Company**                                | Coral Cloud Resorts is a fictitious seaside resort that manages guests and their reservations. It offers a rich set of experiences. |
| **Agent User**                             | New Agent User |
| **Enrich event logs with conversation data** | TRUE |
