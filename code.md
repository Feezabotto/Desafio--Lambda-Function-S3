AWS código lambda. 

Descrição: Processamento de imagens utilizando o s3 e lambda..


    
    import boto3
    from PIL import Image
    import io
    
    s3 = boto3.client('s3')
    
    def lambda_handler(event, context):
        # 1. Pega informações do evento
        fernanda_bucket_origem = event['Records'][0]['s3']['bucket']['name']
        chave_arquivo = event['Records'][0]['s3']['object']['key']
        fernanda_bucket_destino = "bucket-destino-processado"
        
        try:
            # 2. Faz download do objeto do S3
            resposta = s3.get_object(Bucket=fernanda_bucket_origem, Key=chave_arquivo)
            conteudo_arquivo = resposta['Body'].read()
    
            # 3. Abre a imagem em memória
            imagem = Image.open(io.BytesIO(conteudo_arquivo))
    
            # 4. Redimensiona a imagem (ex.: thumbnail 200x200)
            imagem.thumbnail((200, 200))
    
            # 5. Salva em memória
            buffer = io.BytesIO()
            imagem.save(buffer, format="JPEG")
            buffer.seek(0)
    
            # 6. Upload para o bucket de destino
            chave_saida = f"thumbnails/{chave_arquivo}"
            s3.put_object(Bucket=fernanda_bucket_destino, Key=chave_saida, Body=buffer)
    
            return {
                'statusCode': 200,
                'body': f"Thumbnail gerado com sucesso: {chave_saida}"
            }
    
        except Exception as e:
            print(e)
            raise e
