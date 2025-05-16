# CadastraProduto.PHP
Criação do cadastraproduto.php

<?php

include('conn.php');

if($_SERVER['REQUEST_METHOD']=='POST'){
    $nome = $_POST['nome'];
    $descricao = $_POST['descricao'];
    $caracteristica = $_POST['caracteristica'];
    $estoque = $_POST['estoque'];
    $valor = $_POST['valor'];
    $imagem = $_FILES['imagem']['name'];
    $barcode = $_POST['barcode'];
    $status = $_POST['status'];
    
    // Dispensar o uso de If/Else //
  
$sql ="INSERT INTO `tb_produtos`(`nome_produto`, `descricao_produto`, `caracteristica_produto`, `estoque_produto`, `valor_produto`, 
`imagem_produto`, `barcode_produto`, `status_produto`) VALUES ('$nome','$descricao', '$caracteristica', '$estoque', '$valor',
'$imagem', '$barcode', '$status')";

mysqli_query($link,$sql);

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
    <form action="cadastraproduto.php" method="post" enctype="multipart/form-data">
        <label for="nome">Nome:</label>
        <input type="text" name="nome" id="nome" maxlength="50" required>
        <br>
        <label for="descricao">Descrição</label>
        <input type="text" name="descricao" id="descricao" maxlength="150" required>
        <br>
        <label for="caracteristica">Caracteristica:</label>
        <input type="text" name="caracterisitca" id="caracteristica" maxlength="300" required>
        <br>
        <label for="estoque">Estoque:</label>
        <input type="number" name="estoque" id="estoque" maxlength="50" required>
        <br>
        <label for="valor">Valor:</label>
        <input type="number" name="valor" id="valor" maxlength="50" required>
        <br>
        <label for="imagem">Imagem:</label>
        <input type="file" name="imagem" id="imagem" maxlength="5" required>
        <br>
        <label for="barcode">Codigo de Barras:</label>
        <input type="number" name="barcode" id="barcode" maxlength="13" minlength="13">
        <br>
        <input type="submit" value="enviar">
        </div>
    </form>
</body>
</html>
<script>
        document.addEventListener("DOMContentLoaded", function() {
            const cepInput = document.getElementById("cep");
 
  cepInput.addEventListener("blur", function() {
                let cep = cepInput.value.replace(/\D/g, ''); // Remove tudo que não é número
 
  if (cep.length === 8) { // Valida se são 8 dígitos
                    fetch(`https://viacep.com.br/ws/${cep}/json/`)
                        .then(response => {
                            if (!response.ok) {
                                throw new Error('Erro ao buscar o CEP');
                            }
                            return response.json();
                        })
                        .then(data => {
                            if (data.erro) {
                                alert("CEP não encontrado.");
                                return;
                            }
                            // Preenche os campos do formulário
                            document.getElementById("rua").value = data.logradouro;
                            document.getElementById("bairro").value = data.bairro;
                            document.getElementById("cidade").value = data.localidade;
                            document.getElementById("uf").value = data.uf;
                        })
                        .catch(error => {
                            console.error("Erro na busca do CEP: ", error);
                            alert("Não foi possível buscar o endereço.");
                        });
                } else {
                    alert("Formato de CEP inválido. Deve conter 8 dígitos numéricos.");
                }
            });
        });
</script>
