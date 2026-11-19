# Controle de Parcelas

Versão do artefato do Claude para GitHub Pages, usando o Firebase Firestore como banco compartilhado.

## Arquivos

- `index.html`: a página (mesma lógica e visual do artefato)
- `firebase-config.js`: onde vai o config do seu projeto Firebase
- `firestore.rules`: regras de segurança do Firestore

Sem config preenchido, a página roda em "Modo local" (dados só no navegador).

## 1. Firebase (uns 10 min)

1. Acesse https://console.firebase.google.com → **Adicionar projeto** (pode desativar o Analytics).
2. Menu **Criação → Firestore Database → Criar banco de dados**. Escolha a região `southamerica-east1` (São Paulo) e o **modo de produção**.
3. Na aba **Regras** do Firestore, cole o conteúdo de `firestore.rules` e clique em **Publicar**.
4. Engrenagem → **Configurações do projeto → Seus apps → ícone `</>` (Web)**. Registre o app (sem Hosting) e copie o objeto `firebaseConfig` para `firebase-config.js`.

## 2. GitHub Pages

```bash
git init
git add .
git commit -m "Controle de parcelas"
git branch -M main
git remote add origin https://github.com/<seu-usuario>/control-trip.git
git push -u origin main
```

No GitHub: **Settings → Pages → Source: Deploy from a branch → `main` / `(root)`**. Em um ou dois minutos, a página fica no ar em `https://<seu-usuario>.github.io/control-trip/`.

## Teste local

Os módulos ES não carregam via `file://`, então use um servidor local:

```bash
npx serve .
```

## Observações

- O config do Firebase é público por natureza. O que protege o banco são as regras: só a coleção `pagamentos` é acessível, só com os campos e pessoas esperados, e sem edição (só criar ou remover).
- Qualquer pessoa com o link pode registrar ou remover pagamentos, como no artefato. Para restringir, dá para adicionar login com Google depois.
- O "Mês da 1ª parcela" continua salvo por navegador (localStorage), igual ao original.
