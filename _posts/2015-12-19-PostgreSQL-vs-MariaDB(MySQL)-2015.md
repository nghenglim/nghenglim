---
layout: post
title: PostgreSQL vs MariaDB(MySQL) 2015
tags: [DB, benchmark]
---

![PostgreSQL-MySQL]({{ site.baseurl }}/images/2015121900.jpg "PostgreSQL-MySQL")

<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.8.2/jquery.min.js">
</script>
<script src="http://code.highcharts.com/highcharts.js">
</script>
<script src="http://code.highcharts.com/modules/exporting.js">
</script>

<div id="container" style="min-width: 310px; height: 400px; margin: 0 auto">
</div>

<script type="text/javascript">

$(function () {
    $('#container').highcharts({
        chart: {
            type: 'bar'
        },
        title: {
            text: 'PostgreSQL vs MariaDB(MySQL) [QA failed, to be benchmark again]'
        },
        subtitle: {
            text: 'Source: <a href="https://nghenglim.github.io">nghenglim.github.io</a>'
        },
        xAxis: {
            categories: ['Write (10000 rows)', 'Read (Select)', 'READ (WHERE)', 'READ (WHERE A+B>C)', 'READ (COUNT WHERE A+B>C)', 'READ (WHERE ORDER)', 'READ (%wildcard% + ORDER)'],
            title: {
                text: null
            }
        },
        yAxis: {
            min: 0,
            title: {
                text: 'Time Taken (millisecond)',
                align: 'high'
            },
            labels: {
                overflow: 'justify'
            }
        },
        tooltip: {
            valueSuffix: ' millisecond'
        },
        plotOptions: {
            bar: {
                dataLabels: {
                    enabled: true
                }
            }
        },
        legend: {
            layout: 'vertical',
            align: 'right',
            verticalAlign: 'top',
            x: 0,
            y: 90,
            floating: true,
            borderWidth: 1,
            backgroundColor: ((Highcharts.theme && Highcharts.theme.legendBackgroundColor) || '#FFFFFF'),
            shadow: true
        },
        credits: {
            enabled: false
        },
        series: [{
            name: 'MariaDB(MySQL) [10.0.22(5.6.26)]',
            data: [177, 7, 7, 8, 40, 106, 93]
        }, {
            name: 'PostgreSQL [9.2.14]',
            data: [207, 45, 45, 45, 21, 93, 58]
        }]
    });
});

</script>

### Important Notice (11 Feb 2016)
When using pgadmin, the execution time at status bar is including data transfer time, unfortunately, I am using pgadmin status bar execution time to compare with MySQL server execution time which is unfair. I will update the correct benchmark soon.

### Choosing RDBMS
So recently I want to find benchmark for RDBMS between MySQL/MariaDB and PostgreSQL. To my surprise, most benchmark result is outdated, therefore I have decided to benchmark them, using MariaDB(MySQL) [10.0.22(5.6.26)] vs PostgreSQL [9.2.14]

### How to Benchmark
1. Using similar table structure: located at {db}.sql
2. Use python script to generate sql insert data
3. Open sqlyog to benchmark MariaDB(MySQL)
4. Open pgAdmin to benchmark PostgreSQL
5. All setting are using default: setting related file can be found at {benchmark_folder}/{db}_config.txt

You can find the detail at [my Repo](https://github.com/nghenglim/database_benchmark)

### Result
- mariadb(mysql) write (10000 rows): from insert.sql, run 10x time accumulate to 100000 rows
    1. 0.281s
    2. 0.131s
    3. 0.165s
    4. 0.146s
    5. 0.248s
    6. 0.141s
    7. 0.136s
    8. 0.208s
    9. 0.157s
    10. 0.155s

- postgresql write (10000 rows):
    1. 0.227s
    2. 0.256s
    3. 0.215s
    4. 0.227s
    5. 0.194s
    6. 0.195s
    7. 0.203s
    8. 0.205s
    9. 0.174
    10. 0.182s

simple query: taking average of multiple time query

1. `SELECT * FROM testing LIMIT 1000`
    - mariadb(mysql):0.007s
    - postgresql: 0.045s

2. `SELECT * FROM testing WHERE int_col > 5000 LIMIT 1000`
    - mariadb(mysql):0.007s
    - postgresql: 0.045s

3. `SELECT * FROM testing WHERE int_col + int_col2 > 12345`
    - mariadb(mysql): 0.008s
    - postgresql: 0.045s

4. `SELECT COUNT(*) FROM testing WHERE int_col + int_col2 > 12345`
    - mariadb(mysql): 0.040s
    - postgresql: 0.021s

5. `SELECT * FROM testing WHERE int_col > 5000 ORDER BY word_col ASC LIMIT 1000`
    - mariadb(mysql): 0.106s
    - postgresql: 0.093s

6. `SELECT * FROM testing WHERE word_col LIKE '%lim%' ORDER BY word_col DESC LIMIT 1000`
    - mariadb(mysql): 0.093s
    - postgresql: 0.058s

### Conclusion
MariaDB(MySQL) is good at dead simple query, however PostgreSQL is good at more complicated query.

For real world scenario, it will more likely has a lot of complicated query, therefore its better to choose PostgreSQL for it - provided that PostgreSQL comes with lots of useful feature that MySQL lack of.
