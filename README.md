# marvin.bonnano.com.br

Site público do Marvin (página estática).

## Publicação no servidor

No VPS, o conteúdo é publicado em:

- `/var/www/marvin/index.html`

Pipeline (manual por enquanto):

```bash
cp -f ./index.html /var/www/marvin/index.html
```

> Observação: este repositório deve conter **apenas conteúdo público**.
