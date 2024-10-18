# Etapa de construção
FROM alpine:latest AS build

# Instala o Nginx e outras dependências (se necessário)
RUN apk add --no-cache nginx

# Cria um diretório para os arquivos HTML
WORKDIR /app

# Copia os arquivos HTML e de imagem para o diretório de construção
COPY index.html .
COPY logo.png .

# Etapa de produção
FROM nginx:alpine

# Copia os arquivos construídos da etapa anterior
COPY --from=builder /app/index.html /usr/share/nginx/html/index.html
COPY --from=builder /app/logo.png /usr/share/nginx/html/logo.png

# Exclui arquivos de exemplo do Nginx (opcional)
RUN rm -rf /usr/share/nginx/html/*

# Expõe a porta 80 para acesso ao serviço web
EXPOSE 80

# Define o comando padrão para iniciar o Nginx
CMD ["nginx", "-g", "daemon off;"]
