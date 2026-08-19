# Agenda — Rotina & Metas

App pessoal de agenda: rotina diária por horário, lembretes, calendário do mês e metas de longo/médio/curto prazo. Feito só com HTML, CSS e JavaScript puro — não precisa de Node, build, nem backend.

## Arquivos

- `index.html` — o app inteiro (interface + lógica)
- `manifest.json` — descreve o app para o celular poder "instalar" (nome, ícone, cores)
- `service-worker.js` — permite o app carregar offline e ser instalado como PWA
- `icon-192.png` / `icon-512.png` — ícones do app

Os dados (tarefas, lembretes, metas) ficam salvos no `localStorage` do navegador — ou seja, **no aparelho/navegador onde você usa o app**, não numa conta na nuvem. Se limpar os dados do navegador, perde o que foi salvo.

---

## 1. Testar localmente antes de publicar

Não precisa de nada instalado além de um navegador. Duas formas:

**A. Abrir direto**
Dê duplo clique em `index.html`. O app funciona, mas o "Instalar como app" e o modo offline (service worker) só funcionam quando servido por `http://` ou `https://` — não por `file://`.

**B. Rodar um servidor local (recomendado para testar tudo)**
Se tiver Python instalado:
```bash
cd agenda-app
python3 -m http.server 8000
```
Depois abra `http://localhost:8000` no navegador.

Ou, no VS Code, instale a extensão **Live Server** e clique em "Go Live" com `index.html` aberto.

---

## 2. Publicar online (para acessar pelo celular)

Para instalar como app no celular, o site precisa estar em HTTPS. A forma mais simples e gratuita é o **GitHub Pages**.

### Passo a passo — GitHub Pages

1. Crie uma conta no [github.com](https://github.com) (se ainda não tiver).
2. Crie um repositório novo (ex: `agenda-app`), público.
3. Suba os 5 arquivos desta pasta (`index.html`, `manifest.json`, `service-worker.js`, `icon-192.png`, `icon-512.png`) para o repositório:
   - Pelo site: botão **"Add file" → "Upload files"**, arraste os arquivos, clique em **Commit changes**.
   - Ou pelo terminal, se preferir Git:
     ```bash
     cd agenda-app
     git init
     git add .
     git commit -m "primeira versão da agenda"
     git branch -M main
     git remote add origin https://github.com/SEU_USUARIO/agenda-app.git
     git push -u origin main
     ```
4. No repositório, vá em **Settings → Pages**.
5. Em **Source**, selecione a branch `main` e a pasta `/ (root)`. Clique em **Save**.
6. Aguarde 1–2 minutos. Seu app estará em:
   `https://SEU_USUARIO.github.io/agenda-app/`

### Alternativas ao GitHub Pages
- **Netlify** (netlify.com): arraste a pasta inteira na área de deploy do site — fica pronto em segundos, sem precisar de Git.
- **Vercel** (vercel.com): conecta direto num repositório GitHub e publica automaticamente a cada mudança.

Qualquer uma das três funciona igual para este app, já que ele não tem backend.

---

## 3. Instalar no celular como se fosse um app

### Android (Chrome)
1. Abra a URL publicada (ex: `https://SEU_USUARIO.github.io/agenda-app/`) no Chrome.
2. Toque no menu (⋮) no canto superior direito.
3. Toque em **"Instalar app"** (ou "Adicionar à tela inicial").
4. Confirme. O ícone aparece na tela inicial e abre em tela cheia, sem a barra do navegador.

### iPhone (Safari)
1. Abra a URL no Safari (precisa ser Safari, não Chrome, para essa opção aparecer).
2. Toque no ícone de **compartilhar** (quadrado com seta para cima).
3. Toque em **"Adicionar à Tela de Início"**.
4. Confirme o nome e toque em **Adicionar**.

Depois disso, o app abre como qualquer outro instalado: ícone próprio, sem barra de endereço, e funciona mesmo com internet instável (graças ao service worker).

---

## Observações importantes

- **Dados não sincronizam entre aparelhos.** Se você instalar no celular e no notebook, cada um terá sua própria lista salva localmente. Para sincronizar entre dispositivos seria necessário um backend com banco de dados (ex: Firebase, Supabase) — posso ajudar a montar isso se quiser evoluir o app nessa direção.
- **Backup:** como tudo fica no navegador, é uma boa ideia não depender só disso para informações críticas. Se quiser, posso adicionar um botão de "exportar/importar dados" em JSON.
- **HTTPS é obrigatório** para instalar como app — por isso o passo de publicar online é necessário; não dá para instalar direto do arquivo local no celular.
