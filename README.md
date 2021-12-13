# charttikoodi
mun ja daniellan tekemä koodi


























<?php 
       // header("refresh: 3;");
        $hostname = "localhost";
        $username = "root";
        $password = "HyTe";
        $db = "Tiedot";
        $dbconnect=mysqli_connect($hostname,$username,$password,$db);
        if ($dbconnect->connect_error) {
            die("database connection failed: " . $dbconnect->connect_error);
        }
        ?>
  <html>
  <head>
    <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
    <script type="text/javascript">
      google.charts.load('current', {'packages':['corechart']});
      google.charts.setOnLoadCallback(drawChart);

      function drawChart() {
        
        var data = google.visualization.arrayToDataTable([
          ['pvm','arvo'],
         <?php
                  $query = mysqli_query($dbconnect, "SELECT * FROM Mittari ORDER BY id DESC LIMIT 15")
            or die (mysqli_error($dbconnect));
            while ($row = mysqli_fetch_array($query)){
         
         //$moi =  mysqli_query($pvm,$arvo);
         //while ($abc = mysqli_fetch_array($moi)){
         echo "['".$row['pvm']."',".$row['arvo']."],"; 
           
          }
         
         ?> 
          
        ]);

        var options = {
          title: 'apinamafia',
          curveType: 'function',
          legend: { position: 'bottom' }
        };

        var chart = new google.visualization.LineChart(document.getElementById('curve_chart'));

        chart.draw(data, options);
      }
    </script>
  </head>
  <body>
    <div id="curve_chart" style="width: 900px; height: 500px"></div>
  </body>
</html>
