<?php
$conexion=mysqli_connect("localhost","root","","canchas")
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <link rel="stylesheet" type="text/css" href="estilos.css">
    <style type="text/css" >
        td{
            padding: 20px;
        }
        h1{
            text-align: center;
        }
        </style>
    <title></title>
</head>
<body>
    <form action="validar.php" method="post">
    <center>
        <table border="0" bgcolor="#5DADE2" style="width: 100%">
        <td><h1>Bienvenido!!</h1></td>
    </table><br><br>
        <table border="2" bgcolor=#45B39D style="width: 10%">
            <tr><td>Usuario</td><td><input type="text" name="usuario"></td></tr>
            <tr><td>Contraseña</td><td><input type="password" name="contraseña"></td></tr>
</table> <br><br>
<input type="submit" value="Ingresar"></form><br>
</body>
</html>

<?php
$usuario=$_POST['usuario'];
$contraseña=$_POST['contraseña'];
session_start();
$_SESSION['usuario']=$usuario;

include('conexion.php');

$consulta="SELECT*FROM usuarios where usuario='$usuario' and contraseña='$contraseña'";
$resultado=mysqli_query($conexion,$consulta);

$filas=mysqli_fetch_array($resultado);

if($filas['id_cargo']==1){
    header("location:admin.php");

}else
if($filas['id_cargo']==2){
    header("location:cliente.php");
}

mysqli_free_result($resultado);
mysqli_close($conexion);
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <style type="text/css">
        h1{
            text-align: center;
        }
        h4{
            text-align: center;
        }
        </style>
    <title>Cliente</title>
</head>
<body bgcolor=#CD6155>
    <form action="index.php" method="post" style="text-align: right">
        <input type="submit" value="Cerrar sesion"></form>
    <center>
        <table bgcolor=#E6B0AA border=0 style="width: 100%">
    <tr><td><h1>Arriendo de canchas deportivas!!</h1></td></tr></table>
    <h3 style="color: black">Seleccione la cancha que desea arrendar!!</h3><br><br><br>
    <form action="nuevo.php" method="post">
    <div style="width: 400px; height: 200px; border: 1px black solid; background: url('futbol.jpg') no-repeat; background-size: cover;"></div>
    <input type="submit" value="Arrendar" name="arrendar"><br><br>
    <div style="width: 400px; height: 200px; border: 1px black solid; background: url('tenis.jpg') no-repeat; background-size: cover;"></div>
    <input type="submit" value="Arrendar" name="arrendar"><br><br>
    <div style="width: 400px; height: 200px; border: 1px black solid; background: url('basquet.jpg') no-repeat; background-size: cover;"></div>
    <input type="submit" value="Arrendar" name="arrendar"></form>
    
    <!DOCTYPE html>
<html lang="en">
<head>
    <title>Eliminar</title>
</head>
<body bgcolor=#795548>
    <?php

    include('conexion.php');

    $rut = $_POST['RUT'];

    mysqli_query($conexion, "DELETE from reserva where id_cliente='$rut'");

    mysqli_close($conexion);
    ?>
    <table border="0" bgcolor=#A1887F style="width: 100%">
    <tr><td><h1 style="text-align: center">Su reserva se ha eliminado correctamente :(</h1></td></tr></table>
    <form action="cliente.php" style="text-align: center">
        <input type="submit" value="Volver">
    
</body>
</html>
    
    <!DOCTYPE html>
<html lang="en">
<head>
    <title>Arrendar</title>
</head>
<body bgcolor=#76D7C4>
    <center>
        <h1>Ingrese los datos de su arriendo!!</h1>
        <table border="1" bgcolor="#17A589">
            <tr><td>Hora de inicio</td><td><input type="time"></td></tr>
            <tr><td>Hora de termino</td><td><input type="time"></td></tr>
            <tr><td>Fecha de arriendo</td><td><input type="date"></td></tr>
            <tr><td>Rut cliente</td><td><input type="time"></td></tr>
            <tr><td>Numero de cancha</td><td><input type="time"></td></tr>
            <tr><td>Abono</td><td><input type="time"></td></tr>
            <tr><td>Total</td><td><input type="time"></td></tr>
            <tr><td>Forma de pago</td><td><input type="time"></td></tr>
            <tr><td>Rut de empleado</td><td><input type="time"></td></tr>
</table>
    
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
    <title>arrendado</title>
</head>
<body bgcolor=#E74C3C>
    <?php

    include('conexion.php');

    $horainicio = $_POST['horain'];
    $horafin = $_POST['horafin'];
    $fecarriendo = $_POST['fearriendo'];
    $rutcliente = $_POST['rutcli'];
    $numerocancha = $_POST['numcancha'];
    $abono = $_POST['abono'];
    $total = $_POST['total'];
    $formapago = $_POST['formapago'];
    $rutempleado = $_POST['rutempleado'];

    $insertar = "INSERT into reserva values ('$horainicio', '$horafin', '$fecarriendo', '$rutcliente', '$numerocancha', '$abono', '$total', '$formapago', '$rutempleado')";

    $resultado = mysqli_query($conexion, $insertar);

    mysqli_close($conexion);



    ?>
<center>
    <h1>Su arriendo se ha ingresado correctamente!!</h1><br><br>
    <form action="cliente.php">
        <input type="submit" value="Volver al inicio">
</center>    
</body>

</html>

    <form action="modificar.php" method="post" style="text-align: left">
        <h4 style="text-align: left">¿Desea agregar el abono ahora?</h4>
        <h4 style="text-align: left">Ingrese su rut</h4>
        <input type="text" name="Rut">
        <h4 style="text-align: left">Ingrese el monto del abono</h4>
        <input type="text" name="Abono">
        <input type="submit" value="Agregar Abono"></form> 
        
        <form action="eliminar.php" method="post" style="text-align: right"> 
        <h4 style="text-align: right">¿Desea cancelar su reserva?</h4>
        <h4 style="text-align: right">Ingrese su rut</h4>
        <input type="text" name="RUT">
        <input type="submit" value="Eliminar Reserva"></form>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
<link rel="stylesheet" type="text/css" href="estilos.css">
    <style type="text/css">
        td{
            text-align: center;
        }
        </style>
    <title>Admin</title>
</head>
<body>
    <form action="index.php" style="text-align: right">
        <input type="submit" value="Cerrar sesion"></form>
    <center>
        <table bgcolor=#99FF66  border=0 style="width: 100%">
    <td><h1>Bienvenido Administrador!!</h1></td></table><br><br>
    <table bgcolor=#00FF00 border=1 style="padding: 10px black solid; width: 50%">
    <form action="reservas.php" method="post">
        <tr><td><h3>Ver reservas</h3></td><td><input type="submit" value="Ver" name="reservas"></td></tr></form>
        <form action="listaclientes.php" method="post">
        <tr><td><h3>Ver lista de clientes</h3></td><td><input type="submit" value="Ver" name="listaclientes"></td></tr></form>
        <form action="deletereserva.php" method="post">
        <tr><td><h3>Eliminar una reserva</h3></td><td><h5>Ingrese el rut del cliente</h5><input type="text" name="RUt"><br><input type="submit" value="Eliminar" name="eliminar"></td></tr></form>
    </table>
</table>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
    <title>Reservas</title>
</head>
<body bgcolor=#33FFFF>
    <center>
        <h1>Lista de reservas</h1>
        <?php
        if($_POST['reservas']=="Ver")
        {

        include('conexion.php');
        $cnn = conectar[];
        $rs= mysqli_query("SELECT * from reserva", $cnn);
        echo "<table text-align: center; border="1">";
        echo "<tr>";
        echo "<td><b>Hora de inicio</td></b>";
        echo "<td><b>Hora de termino</td></b>";
        echo "<td><b>Fecha de arriendo</td></b>";
        echo "<td><b>Rut Cliente</td></b>";
        echo "<td><b>Numero de Cancha</td></b>";
        echo "<td><b>Abono</td></b>";
        echo "<td><b>Total</td></b>";
        echo "<td><b>Forma de pago</td></b>";
        echo "<td><b>Rut empleado</td></b>";
        echo "</tr>";
        
        while ($row = mysqli_fetch_array($rs))
        {
            echo "<tr>";
            echo "<td> $row['hora_inicio']</td>";
            echo "<td> $row['hora_fin']</td>";
            echo "<td> $row['fecha']</td>";
            echo "<td> $row['id_cliente']</td>";
            echo "<td> $row['id_cancha']</td>";
            echo "<td> $row['abono']</td>";
            echo "<td> $row['total']</td>";
            echo "<td> $row['formapago']</td>";
            echo "<td> $row['id_empleado']</td>";
        }
        echo "</tables>";
        }
        ?>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
    <title>Reservas</title>
</head>
<body bgcolor=#33FFFF>
    <center>
        <h1>Lista de reservas</h1>
        <?php
        if($_POST['listaclientes']=="Ver")
        {

        include('conexion.php');
        $rs= mysqli_query("SELECT * from clientes");
        echo "<table text-align: center; border="1">";
        echo "<tr>";
        echo "<td><b>Rut cliente</td></b>";
        echo "<td><b>Nombre</td></b>";
        echo "<td><b>Apellido</td></b>";
        echo "<td><b>Fecha de nacimiento</td></b>";
        echo "<td><b>Direccion</td></b>";
        echo "<td><b>Fono</td></b>";
        echo "<td><b>Correo</td></b>";
        echo "</tr>";
        
        while ($row = mysqli_fetch_array($rs))
        {
            echo "<tr>";
            echo "<td> $row['rut']</td>";
            echo "<td> $row['nombre']</td>";
            echo "<td> $row['apellido']</td>";
            echo "<td> $row['fnac']</td>";
            echo "<td> $row['direccion']</td>";
            echo "<td> $row['fono']</td>";
            echo "<td> $row['mail']</td>";
        }
        echo "</tables>";
        }
        ?>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
    <title>deletereserva</title>
</head>
<body bgcolor=#99FF00>
<?php

include('conexion.php');

$rut = $_POST['RUt'];
$eliminar = $_POST['eliminar'];

mysqli_query($conexion, "DELETE from reserva where id_cliente='$rut'");

mysqli_close($conexion);

?>
    <table border="0" bgcolor=#33FF00 style="width: 100%">
        <tr><td><h1 style="text-align: center">La reserva se ha eliminado correctamente</h3></td></tr></table>
        <form action="admin.php" style="text-align: center">
            <input type="submit" value="Volver"></form>
    
</body>
</html>

body{
    background: url(canchas.jpg);   
    background-position: center;
    font-family: sans-serif;
    }
body{
    background: url(canchas.jpg);
    background-position: center;
    font-family: sans-serif;
}
