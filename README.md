# SQL_sreya_2337016
SQL queries including join

1.	Display all the attributes of the data.
select * from weathersource-com.pub_weather_data_samples.sample_weather_forecast_great_britain_postalcode_daily
![image](https://github.com/RithikaSreya/SQL_sreya_2337016/assets/159041623/5c0f0320-47eb-40df-8b6e-9f8f728221e8)

2.	Get max, min and average air temperature for GB country.
select country,avg(max_temperature_air_2m_f) as avg_max_temp,avg(min_temperature_air_2m_f) as avg_min_temp,avg(avg_temperature_air_2m_f) as avg_temp from weathersource-com.pub_weather_data_samples.sample_weather_forecast_great_britain_postalcode_daily where country='GB' group by 1
 ![image](https://github.com/RithikaSreya/SQL_sreya_2337016/assets/159041623/e639ab61-1142-404d-b8a5-527f88c0cd83)

3.	What all unique postal codes are included in data?
select distinct postal_code from weathersource-com.pub_weather_data_samples.sample_weather_forecast_great_britain_postalcode_daily
 ![image](https://github.com/RithikaSreya/SQL_sreya_2337016/assets/159041623/a69b9757-efa4-4dbf-a14e-af1e1d1b2716)

4.	Find top 8 max pressure postal codes with max pressure, min pressure, avg_pressure.
select  postal_code, avg(max_pressure_2m_mb) as avg_max_pressure,avg(min_pressure_2m_mb)as avg_min_pressure,avg(avg_pressure_2m_mb) as avg_pressure from weathersource-com.pub_weather_data_samples.sample_weather_forecast_great_britain_postalcode_daily group by postal_code order by avg_max_pressure desc limit 8
![image](https://github.com/RithikaSreya/SQL_sreya_2337016/assets/159041623/57dd79ec-6184-4792-9456-baa55489011b)

5.	What are the total crimes in US.
select country, sum(num_crimes) as crimes from weathersource-com.pub_weather_data_samples.sample_weather_and_crime_comparison_chicago_daily_2016 where country = 'US' group by 1
![image](https://github.com/RithikaSreya/SQL_sreya_2337016/assets/159041623/25016e72-99ae-4ebb-84b7-b911d6688435)

6.	Get the crimes of first week of June in US.
select country,cast(date_valid_std as date) as crimedate, sum(num_crimes) as crimes from weathersource-com.pub_weather_data_samples.sample_weather_and_crime_comparison_chicago_daily_2016 where date_valid_std BETWEEN '2016-06-01' and '2016-06-07' group by 1,2 order by crimedate asc
 ![image](https://github.com/RithikaSreya/SQL_sreya_2337016/assets/159041623/94d7d234-0564-4ab1-b15d-2a92856f4758)

7.	Which month has highest crimes in US.
select EXTRACT(month FROM date_valid_std ) AS month,country, sum(num_crimes) as crimes from weathersource-com.pub_weather_data_samples.sample_weather_and_crime_comparison_chicago_daily_2016 group by 1,2 order by crimes desc limit 1
![image](https://github.com/RithikaSreya/SQL_sreya_2337016/assets/159041623/bb6bea81-9169-45fc-87b4-d61ac853492a)

8.	Which month has minimum crimes in US.
select EXTRACT(month FROM date_valid_std ) AS month,country, sum(num_crimes) as crimes from weathersource-com.pub_weather_data_samples.sample_weather_and_crime_comparison_chicago_daily_2016 group by 1,2 order by crimes asc limit 1
 ![image](https://github.com/RithikaSreya/SQL_sreya_2337016/assets/159041623/8e2dba3b-00d2-4627-97d2-c3396bfcd6db)

9.	Use inner join to get all the common columns of both the dataset.
select * from 
weathersource-com.pub_weather_data_samples.sample_weather_forecast_us_zipcode_daily a
inner join
weathersource-com.pub_weather_data_samples.sample_weather_forecast_anomaly_us_zipcode_daily b
on a.postal_code=b.postal_code and a.date_valid_std=b.date_valid_std
![image](https://github.com/RithikaSreya/SQL_sreya_2337016/assets/159041623/3d485efa-76ea-4b50-87d2-03f997238377)

10.	What is the average wind direction degree as per anomaly wind.
select a.postal_code,a.date_valid_std as date,avg(avg_wind_direction_10m_deg) as wind_direc, avg(avg_wind_speed_10m_anomaly_mph) as anomaly_windspeed from 
weathersource-com.pub_weather_data_samples.sample_weather_forecast_us_zipcode_daily a
inner join
weathersource-com.pub_weather_data_samples.sample_weather_forecast_anomaly_us_zipcode_daily b
on a.postal_code=b.postal_code and a.date_valid_std=b.date_valid_std
group by 1,2
![image](https://github.com/RithikaSreya/SQL_sreya_2337016/assets/159041623/26c08d73-a2bd-4261-9839-9e18f40f98a2)

11.	What are the min and max pressure for anomaly temperature?
select a.postal_code,a.date_valid_std as date,avg(min_pressure_2m_mb) as min_pressure,avg(max_pressure_2m_mb) as max_pressure, avg(avg_temperature_anomaly_air_2m_f) as anomaly_temperature from 
weathersource-com.pub_weather_data_samples.sample_weather_forecast_us_zipcode_daily a
inner join
weathersource-com.pub_weather_data_samples.sample_weather_forecast_anomaly_us_zipcode_daily b
on a.postal_code=b.postal_code and a.date_valid_std=b.date_valid_std
group by 1,2
![image](https://github.com/RithikaSreya/SQL_sreya_2337016/assets/159041623/fce45eb0-2e60-406b-aaef-d4014bdb1793)
