# valute_airflow_dag
The airflow DAG project on a daily schedule (in cron format: '0 14 * * *') gets updated API data about currency rates from 2 resources, creates reports based on these data, and sends it with a telegram bot.

### The structure of the project's DAG:
1) get_cbr_api_data

    Getting data about currency rates from <a href="[https://www.cbr-xml-daily.ru/daily_json.js]" target="_blank">open API</a> in the 'RUB' base.
2) check_cbr_api_data

    Checking data for validity from the 1-st point.
3) get_cbr_daily_report

    Creating a daily report in .csv format on currency changes (in comparison with yesterday) based on the checked data from point 2.
4) get_fixer_api_data

    Getting data about currency rates for the last 7 days from another <a href="[https://apilayer.com/]" target="_blank">open API</a> in the 'RUB' base.
5) check_fixer_api_data

    Checking data for validity from point 4.
6) get_fixer_daily_report

    Creating a daily report in .csv format on currency changes (in comparison with yesterday) based on the checked data from point 2. It is the 'plan B' report that was made in case of crushing get_cbr_daily_report function.
7) get_fixer_weekly_report

    Creating a report in .csv format, that calculates different metrics for every value for the last 7 days: mean, median, dispersion, min, and max.
8) send_dag_report_from_bot

    Sending all reports (points 4, 6, and 7) from the telegram bot to personal dialog. If some report was crushed during execution, a notification about failure would be sent.

![](https://github.com/Elias0101/valute_airflow_dag/blob/main/images/DAG%20structure.png)
*tasks in valute_airflow_dag*

### Tasks execution report
![](https://github.com/Elias0101/valute_airflow_dag/blob/main/images/Tasks%20execution%20report.png)

### Bot report example
![](https://github.com/Elias0101/valute_airflow_dag/blob/main/images/bot%20report%20example.png)

### Gotten data in .csv formats
![](https://github.com/Elias0101/valute_airflow_dag/blob/main/images/final%20documents.png)
