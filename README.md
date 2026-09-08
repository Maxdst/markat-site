# Markat Engenharia — Site Institucional

Site institucional da **Markat Engenharia**: soluções em engenharia civil,
manutenção industrial e estruturas metálicas para clientes públicos e privados.

> +100 projetos entregues · +25 clientes satisfeitos

---

## 📁 Estrutura do projeto

```
markat-site/
├── index.html                     # Página principal do site
├── markat-site-single-file.html   # Versão do site em arquivo único (tudo embutido)
├── assets/
│   ├── css/style.css              # Estilos
│   ├── js/script.js               # Scripts
│   └── img/                       # Imagens (obras, clientes, logo)
└── README.md
```

É um site **estático** (HTML/CSS/JS puro), sem etapa de build. Basta abrir o
`index.html` no navegador ou servi-lo por qualquer servidor de arquivos estáticos.

## ▶️ Rodar localmente

Abrindo direto o arquivo:

```bash
# abra index.html no navegador
```

Ou servindo por HTTP (recomendado, evita bloqueios de caminhos relativos):

```bash
# Python 3
python3 -m http.server 8080
# depois acesse http://localhost:8080
```

---

## 🌐 Situação do domínio (por que o site não abre)

O erro que aparece ao acessar o site — **`DNS_PROBE_FINISHED_NXDOMAIN`** —
significa que o **nome de domínio não resolve no DNS**: ele não aponta para
nenhum servidor. Não é problema do navegador nem do computador de quem acessa.

### O que foi verificado

| Domínio | Resultado |
|---|---|
| `grupomarkat.com` | **Não resolve** (NXDOMAIN / `ENOTFOUND`) — o `.com` não tem DNS configurado |
| `grupomarkat.com.br` | Relatado como **fora do ar** também |

Observação importante: o próprio site usa o e-mail **`contato@grupomarkat.com.br`**
(veja o `index.html`), ou seja, o domínio pretendido pela empresa é o **`.com.br`**.

### Causas prováveis (a confirmar no registrador)

1. **Domínio expirado.** Se o registro no [registro.br](https://registro.br)
   (para `.com.br`) ou no registrador do `.com` venceu, o domínio para de
   resolver. É a causa mais comum quando um site que funcionava sai do ar.
2. **DNS/nameservers sem apontamento.** O domínio existe, mas não há
   registros **A/CNAME** válidos, ou os **nameservers** não estão apontando
   para a hospedagem.
3. **Hospedagem desativada.** O domínio resolve, mas o servidor de destino
   não responde (nesse caso o erro seria de conexão, não NXDOMAIN).
4. **TLD errado.** Confundir `.com` com `.com.br`. O `.com` **não** está
   registrado/configurado; o oficial é o `.com.br`.

### Como diagnosticar (rode na SUA máquina)

```bash
# O domínio resolve? (troque pelo domínio que você quer testar)
nslookup grupomarkat.com.br
nslookup grupomarkat.com

# Registros detalhados (Linux/macOS)
dig grupomarkat.com.br A
dig grupomarkat.com.br NS
dig grupomarkat.com.br SOA
```

- Se `nslookup`/`dig` responder **"NXDOMAIN"** ou **"can't find"** → o domínio
  não está registrado ou está sem DNS. Vá ao registrador.
- Se responder um **IP** mas o site não abrir → o DNS está ok, o problema é a
  **hospedagem** (servidor fora do ar ou apontando errado).

### Verificar registro/expiração

- **`.com.br`**: consulte em <https://registro.br/busca-dominio/> (mostra se
  está registrado, o titular e a data de expiração).
- **`.com`**: consulte o WHOIS do registrador onde foi comprado (GoDaddy,
  Namecheap, etc.) ou em <https://lookup.icann.org/>.

### Como resolver

1. **Renovar o domínio** se estiver expirado.
2. **Configurar o DNS** apontando um registro **A** (para o IP da hospedagem)
   ou **CNAME** (para o host da hospedagem) — incluindo o subdomínio `www`.
3. Se quiser publicar **este repositório** como site, veja a seção abaixo.

---

## 🚀 Publicar via GitHub Pages (opcional)

Como o site é estático, dá para hospedá-lo de graça no GitHub Pages:

1. No GitHub: **Settings → Pages**.
2. Em **Source**, escolha a branch (`master`) e a pasta **/(root)**.
3. Salve. O site ficará disponível em `https://<usuario>.github.io/markat-site/`.
4. Para usar o domínio próprio (`grupomarkat.com.br`):
   - Adicione um arquivo **`CNAME`** na raiz do repositório com o domínio
     (ex.: `grupomarkat.com.br`).
   - No DNS do domínio, crie os registros apontando para o GitHub Pages:
     - `A` → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
     - `CNAME` do `www` → `<usuario>.github.io`
   - Documentação: <https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site>

> **Importante:** o GitHub Pages só serve o site; ele **não registra nem renova
> o domínio**. O passo do registro/renovação no registrador continua sendo
> obrigatório para o domínio voltar a funcionar.

---

## 📇 Contato

- **E-mail:** contato@grupomarkat.com.br
