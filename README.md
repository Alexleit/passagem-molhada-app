# Vistoria de Passagem Molhada — projeto Android (Capacitor)

Este pacote transforma o app web (o mesmo HTML que já vem sendo usado como PWA)
em um projeto Android nativo, pronto para gerar um `.apk` de verdade.

O app em si (formulário, fotos, PDF, senha, IndexedDB) é exatamente o mesmo — só
está empacotado dentro de um "casco" Android (via Capacitor).

## Caminho recomendado: gerar o APK na nuvem (sem instalar nada no seu PC)

Este pacote já vem com um "robô" configurado (GitHub Actions) que compila o
APK automaticamente em um servidor do GitHub — você só precisa subir os
arquivos, sem instalar Android Studio nem nada parecido.

### Passo 1 — Criar uma conta no GitHub (gratuita)
Se ainda não tiver: https://github.com/signup

### Passo 2 — Criar um repositório novo
- No canto superior direito do GitHub, clique em **+ → New repository**
- Dê um nome, por exemplo `passagem-molhada-app`
- Pode deixar como **Private** (só você vê) ou Public, tanto faz
- Não marque nenhuma opção de "adicionar README" — deixe vazio
- Clique em **Create repository**

### Passo 3 — Subir os arquivos deste pacote
Na página do repositório recém-criado, vai ter um link **"uploading an
existing file"** (ou **Add file → Upload files** no menu). Clique nele e
arraste **todo o conteúdo desta pasta** (incluindo a pasta `android/`, a
pasta `www/`, a pasta `.github/`, e os arquivos soltos como
`capacitor.config.ts` e `package.json`) para dentro da área de upload.

Espere o upload terminar e clique em **Commit changes** (botão verde,
embaixo).

> Dica: se o navegador reclamar de "muitos arquivos", o mais garantido é
> usar o app **GitHub Desktop** (também gratuito, https://desktop.github.com) —
> nele você só aponta pra essa pasta no seu computador e clica em "Publish
> repository", sem precisar arrastar arquivo por arquivo.

### Passo 4 — Aguardar o robô compilar
Depois do commit, clique na aba **Actions** (no topo do repositório). Vai
aparecer uma execução chamada "Build Android APK" rodando (bolinha amarela
girando). Isso demora de **3 a 6 minutos**. Quando terminar, o ícone fica
verde ✅.

### Passo 5 — Baixar o APK pronto
Clique em cima dessa execução já finalizada (verde). Role até o final da
página — vai ter uma seção **Artifacts** com um item chamado
**passagem-molhada-apk**. Clique para baixar — vem um `.zip` contendo o
`app-debug.apk` dentro.

Transfira esse `.apk` pro celular (Google Drive, WhatsApp, cabo USB, etc.) e
instale — pode ser necessário permitir "instalar de fontes desconhecidas"
nas configurações do Android, já que não veio da Play Store.

### Se precisar atualizar o app depois
Sempre que eu (ou você) editar o `www/index.html`, é só subir a versão nova
desse arquivo pro mesmo repositório (substituindo o antigo) — o robô do
GitHub Actions roda de novo sozinho e gera um APK atualizado.

---

## Caminho alternativo: Android Studio na sua máquina

Se preferir compilar localmente em vez de usar a nuvem:

### 1. Instalar o Android Studio
Baixe em https://developer.android.com/studio (gratuito). Ele já vem com o
Android SDK e o Gradle — não precisa instalar nada separado.

### 2. Abrir o projeto
No Android Studio: **File → Open** → selecione a pasta `android/` deste pacote
(não a pasta raiz, a pasta `android` dentro dela).

Na primeira vez, o Android Studio vai baixar automaticamente algumas
dependências (isso precisa de internet, mas é automático — só aguardar a
barra de progresso "Gradle Sync" terminar, alguns minutos).

### 3. Gerar o APK
Com o projeto aberto:
- Menu **Build → Build Bundle(s) / APK(s) → Build APK(s)**
- Quando terminar, aparece um aviso "APK(s) generated successfully" com um
  link **locate** — clique para achar o arquivo, algo como:
  `android/app/build/outputs/apk/debug/app-debug.apk`

## Outros detalhes do projeto

- Nome do app: **Vistoria Passagem Molhada**
- ID do pacote: **br.geophocus.passagemmolhada**
- Permissões de Câmera e Localização já declaradas.
- Plugin oficial **@capacitor/geolocation** já instalado e sincronizado
  (o GPS funciona tanto no navegador quanto dentro do app empacotado).

### (Opcional) Ícone do app
O app está usando o ícone padrão do Capacitor por enquanto. Se quiser usar a
logo do projeto como ícone, me avise — eu preparo os arquivos de ícone
redimensionados (o Android pede vários tamanhos) e te aviso onde colocar em
`android/app/src/main/res/`.

### (Opcional) Assinar e gerar um APK/AAB "de produção"
O passo acima gera um APK de **debug** (bom pra testar no seu celular). Se um
dia quiser publicar na Play Store, o Android Studio tem um assistente pronto
para isso em **Build → Generate Signed Bundle / APK**, que cria uma chave de
assinatura própria sua.

---

Qualquer erro que aparecer (no Actions ou no Gradle Sync do Android Studio),
me manda a mensagem de erro que eu te ajudo a resolver.
