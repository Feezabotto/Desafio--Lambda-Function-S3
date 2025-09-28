Quinto desafio do curso Code Girl da Dio.

## Introdução
Repositório com anotações sobre os serviços AWS S3 e Lambda, além de um workflow prático que exemplifica um caso de uso integrando ambos os serviços.

## O que é o Amazon S3?
O Amazon S3 é um dos principais componentes da AWS. É anunciado como um armazenamento com “escalabilidade infinita”. Permite que as pessoas armazenem objetos (arquivos) em “buckets” (diretórios)

Algumas características:
• Os buckets devem ter um nome globalmente exclusivo (em todas as regiões e contas)
• Os buckets são definidos no nível da região
• O S3 parece um serviço global, mas os buckets são criados em uma região
• Sem letras maiúsculas, sem sublinhados
• 3 a 63 caracteres de comprimento
• Não pode ser um IP
• Deve começar com letra minúscula ou número
• NÃO deve começar com o prefixo xn--
• NÃO deve terminar com o sufixo -s3alias

## **S3 - Objetos**

• Os objetos (arquivos) tem uma chave

• A chave é o caminho COMPLETO: 

```bash
s3://my-bucket/my_file.txt
s3://my-bucket/my_folder1/another_folder/my_file.txt
```

• A chave é composta por **prefixo** + **nome do objeto**

```bash
s3://my-bucket/my_folder1/another_folder/my_file.txt
```

## **S3 - Políticas**

Políticas baseadas em JSON:

  • **Recursos:** buckets e objetos 

  • **Efeito:** Permitir/Negar 

  • **Ações:** Conjunto de API para Permitir ou Negar • Principal: A conta ou usuário ao qual aplicar a
    política

A política no bucket é utilizado para: 

  • Conceder acesso público ao bucket

  • Forçar a criptografia dos objetos no upload 

  • Conceder acesso a outra conta (Conta cruzada)
  • Conceder acesso a um usuário ou conta específica

```bash
{
		"Version": "2012-10-17",
		"Statement: [
		{ 
			"Sid": "PublicRead",
			"Effect": "Allow",
			"Principal": "*",
			"Action": [
					"s3:GetObject"
			],
			"Resource": [
					"arn:aws:s3:::examplebucket/*"
			]
		}
	]
}
```

## **S3 - Website estático**

O S3 pode hospedar sites estáticos e torná-los acessíveis na internet:
  • A URL do site será (dependendo da região):
    Ex: [http://demo-bucket.s3-website.us-west-2.amazonaws.com]

## O que é o Lambda?
AWS Lambda é o serviço de computação sem servidor (serverless) que permite executar código em resposta a eventos.

## Requisitos
Conta da AWS.
Permissões no IAM para criação e execução do lambda/s3.

## Workflow Design
Um exemplo de processamento de imagens utilizando o s3 e lambda.

## Anexos
code.md contendo o código do template para a criação do workflow e a pasta images contendo o diagrama.

