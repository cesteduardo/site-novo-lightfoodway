# Light Food Way

Site institucional da **Light Food Way**, rede de refeições saudáveis ultracongeladas.
É um site estático: só HTML, CSS e JavaScript, sem servidor, sem banco de dados e sem etapa de build.
Basta colocar os arquivos no ar para ele funcionar.

<br>

## Como as pastas estão organizadas

```
lightfoodway/
├── index.html                    Página inicial
├── nossas-linhas.html            Linhas de produtos e cardápios
├── como-funciona.html            Como comprar e preparar
├── unidades.html                 Mapa e busca de lojas por CEP
├── sobre.html                    História da marca
├── faq.html                      Perguntas frequentes
├── expansao.html                 Seja um franqueado (formulário de leads)
├── politica-de-privacidade.html
├── termos-de-uso.html
├── robots.txt                    Orientação para buscadores
├── sitemap.xml                   Lista de páginas para o Google
├── README.md                     Este guia
│
├── css/                          Visual do site
│   ├── style.min.css             Estilo de todas as páginas
│   ├── page-transitions.min.css  Transição suave entre páginas
│   └── expansao.min.css          Complemento da página de expansão
│
├── js/                           Comportamento do site
│   ├── main.min.js               Menu, animações e comportamento geral
│   ├── page-transitions.min.js   Transição entre páginas
│   ├── hero-titulos.min.js       Animação dos títulos da capa
│   ├── linhas-modal.min.js       Janela de cada linha e visualizador de cardápio
│   ├── mapa-brasil.min.js        Desenho do mapa
│   ├── unidades.min.js           Lista de unidades e busca por CEP
│   └── expansao.min.js           Envio do formulário e botões de WhatsApp
│
├── fonts/                        Inter e Bricolage Grotesque, hospedadas aqui mesmo
│
├── img/                          Imagens do site
│   ├── banners/                  Capas da página inicial e de Nossas Linhas
│   ├── capas/                    Capas das páginas internas
│   ├── linhas/                   Fotos de cada linha de produtos
│   ├── marca/                    Logo, mascote e imagem de compartilhamento
│   ├── icones/                   Favicons e símbolo da GR Brands
│   ├── selos/                    Selos ABF e eureciclo
│   └── texturas/                 Padrões de fundo
│
├── cardapios/                    Páginas dos catálogos em imagem, uma pasta por catálogo
│   ├── marmitas/
│   ├── salgados/
│   ├── sucos/
│   └── doces/
│
└── pdf/                          Catálogos completos para download
```

A regra é simples: **páginas na raiz e cada tipo de arquivo na sua própria pasta.**

<br>

## Como subir pelo GitHub (sem usar terminal)

O navegador aceita até 100 arquivos por envio, e nenhuma pasta do site passa disso.
Por isso dá para subir **uma pasta de cada vez**, sem quebrar o caminho dos arquivos.

| Envio | O que arrastar | Arquivos |
|---|---|---|
| 1 | Os arquivos soltos da raiz (`.html`, `robots.txt`, `sitemap.xml`, `README.md`) | 12 |
| 2 | Pasta `css` | 3 |
| 3 | Pasta `js` | 7 |
| 4 | Pasta `fonts` | 2 |
| 5 | Pasta `img` | 47 |
| 6 | Pasta `cardapios` | 67 |
| 7 | Pasta `pdf` | 4 |

Para cada envio:

1. No repositório, clique em **Add file › Upload files**.
2. Arraste a pasta inteira (ou os arquivos soltos, no primeiro envio).
3. Clique em **Commit changes**.

Os envios 2, 3 e 4 também podem ir juntos, numa leva só.

> Arraste as pastas pelo Chrome ou pelo Edge. Alguns navegadores soltam os arquivos sem as pastas, e aí os caminhos quebram.

Depois do último envio, ative a publicação em **Settings › Pages**, escolhendo a branch `main` e a pasta `/ (root)`.
Em um ou dois minutos o site está no ar. A cada envio novo, o GitHub publica sozinho; dá para acompanhar na aba **Actions**.

**Nas próximas atualizações,** envie só o que mudou. Arquivos com o mesmo nome e caminho são substituídos.
Para apagar um arquivo pelo site do GitHub, abra o arquivo, clique nos três pontos **…** e escolha **Delete file**.

<br>

## Como testar no computador

Abrir o `index.html` com dois cliques funciona, mas o mapa de unidades e os cardápios precisam de um servidor local.
Na pasta do site, rode:

```
python3 -m http.server 8000
```

Depois abra [localhost:8000](http://localhost:8000) no navegador.

<br>

## Ajustes do dia a dia

**Trocar um texto.**
Os textos ficam direto nos arquivos `.html`. Abra a página, procure a frase e edite.

**Atualizar um cardápio.**
Cada catálogo tem duas formas:

* o PDF completo, em `pdf/`, que o visitante baixa;
* as páginas soltas em imagem, em `cardapios/<catálogo>/01.webp, 02.webp…`, que aparecem no visualizador do site.

Quais páginas aparecem em cada linha está anotado em `js/linhas-modal.min.js`, no campo `paginas`.
Ao trocar um PDF, atualize também o campo `tamanho` no mesmo arquivo, que é o peso mostrado no botão de download.

**Garantir que o visitante veja a versão nova.**
Os arquivos de CSS e JS são chamados com um sufixo de versão, como `style.min.css?v=2026-10-16`.
Depois de editar um deles, troque essa data no `<link>` ou no `<script>` das páginas.
Isso obriga o navegador a baixar o arquivo de novo em vez de usar a cópia guardada.

**Mudar o WhatsApp da expansão.**
O número fica em `js/expansao.min.js`. Procure por `5517991458142` e troque pelo novo, sempre no formato `55 + DDD + número`, só com dígitos.

<br>

## Formulário de expansão

Como o site não tem servidor, o formulário de quem quer abrir uma franquia envia os dados
direto do navegador para um **Google Apps Script**, que grava cada contato numa planilha.

* O endereço do script está em `js/expansao.min.js`.
* O código do script e a planilha ficam **fora deste repositório**, porque o repositório é público.
* Ao alterar o script no Google, crie uma **nova versão da implantação**. Assim o endereço continua o mesmo e o site não precisa mudar.

<br>

## O que já foi otimizado

* Imagens em **WebP**, com versões menores (`-900`) para telas de celular.
* Fontes hospedadas no próprio site, sem depender do Google Fonts.
* CSS e JS minificados.
* Catálogos em PDF recomprimidos, de 43 MB para 14 MB, sem mudar o texto nem o layout.
* O mapa de unidades só é carregado quando o visitante chega até ele.
* Nenhuma biblioteca externa: o site inteiro pesa menos de 30 MB, e a maior parte disso são os catálogos para download.

<br>

---

Desenvolvido por **GR Brands.**
