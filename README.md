# CadastraProduto.PHP
Criação do cadastraproduto.php

<?php
// Inclui o arquivo de segurança para administradores //
include('segurancadez.php');

// Inclui o cabeçalho padrão do site //
include('cabecalho.php');

// Conecta ao banco de dados //
include('conn.php');

// Verifica se o formulário foi enviado via POST //
if($_SERVER['REQUEST_METHOD']=='POST'){
    // Captura os dados do formulário //
    $nome = $_POST['nome'];
    $descricao = $_POST['descricao'];
    $caracteristica = $_POST['caracteristica'];  // Note: cuidado com erro de digitação no name no formulário //
    $estoque = $_POST['estoque'];
    $valor = $_POST['valor'];
    $imagem = $_FILES['imagem']['name']; // Nome do arquivo de imagem //
    $barcode = $_POST['barcode'];
    $status = 1; // Produto ativo por padrão //

    // Monta a query para inserir os dados no banco //
    $sql ="INSERT INTO `tb_produtos`(
        `nome_produto`, `descricao_produto`, `caracteristica_produto`, `estoque_produto`, `valor_produto`, 
        `imagem_produto`, `barcode_produto`, `status_produto`) 
        VALUES ('$nome','$descricao', '$caracteristica', '$estoque', '$valor',
        '$imagem', '$barcode', '$status')";

    // Executa a query //
    mysqli_query($link,$sql);

    // Fecha a conexão e redireciona //
    mysqli_close($link);
    header('location: listaprodutos.php');
    exit();
}
?>
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="cadastra.css">
    <title>Cadastra Produto</title>
</head>
<body>
    <div class="container">
        <h1>Cadastra Produto</h1>
        <br>
        <!-- Formulário de envio de dados do produto -->
        <form action="cadastraproduto.php" method="post" enctype="multipart/form-data">
            <label for="nome">Nome:</label>
            <input type="text" name="nome" id="nome" maxlength="50" required>
            <br>

<label for="descricao">Descrição</label>
            <input type="text" name="descricao" id="descricao" maxlength="150" required>
            <br>

<label for="caracteristica">Característica:</label>
            <input type="text" name="caracteristica" id="caracteristica" maxlength="300" required>
            <br>

<label for="estoque">Estoque:</label>
            <input type="number" name="estoque" id="estoque" required>
            <br>

<label for="valor">Valor:</label>
            <input type="number" name="valor" id="valor" step="0.01" required>
            <br>

<label for="imagem">Imagem:</label>
            <input type="file" name="imagem" id="imagem" required>
            <br>

<label for="barcode">Código de Barras:</label>
            <input type="number" name="barcode" id="barcode" maxlength="13" minlength="13">
            <br>

<input type="submit" value="enviar">
        </form>
    </div>
</body>
</html>
