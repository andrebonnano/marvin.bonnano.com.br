# marvin.bonnano.com.br

Site público do Marvin (página estática).

## Estrutura atual no servidor

O projeto está organizado dentro do padrão de projetos próprios em `/opt/projetos`:

```text
/opt/projetos/marvin-site/
  dev/   → ambiente de desenvolvimento
  prod/  → ambiente de produção
```

Ambiente de desenvolvimento (onde trabalhamos nos arquivos):

```text
/opt/projetos/marvin-site/dev/
  README.md
  index.html
  ... (outros arquivos estáticos do site)
```

Ambiente de produção (servido pelo Caddy):

```text
/opt/projetos/marvin-site/prod/
  index.html
  ... (versão publicada)
```

## Endereços

- Produção: `https://marvin.bonnano.com.br`
- Desenvolvimento: `https://marvin.bonnano.com.br/desenv`

O Caddy está configurado assim:

```caddyfile
marvin.bonnano.com.br {
    encode gzip

    @dev path /desenv*
    handle @dev {
        root * /opt/projetos/marvin-site/dev
        try_files {path} /index.html
        file_server
    }

    handle {
        root * /opt/projetos/marvin-site/prod
        try_files {path} /index.html
        file_server
    }
}
```

## Pipeline de publicação

Fluxo sugerido:

1. Editar e testar o site em desenvolvimento:
   - arquivos em `/opt/projetos/marvin-site/dev/`
   - visualizar em `https://marvin.bonnano.com.br/desenv`

2. Quando estiver aprovado, publicar em produção copiando o conteúdo de `dev` para `prod`:

   ```bash
   sudo rsync -a --delete \
     /opt/projetos/marvin-site/dev/ \
     /opt/projetos/marvin-site/prod/
   ```

3. Conferir produção em `https://marvin.bonnano.com.br`.

> Observação: este repositório deve conter **apenas conteúdo público**. Qualquer lógica de backend ou dados sensíveis devem ficar fora desta árvore.

