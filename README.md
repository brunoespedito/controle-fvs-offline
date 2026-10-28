# Controle FVS — pacote GitHub com PWA e fila offline

## Arquivos deste repositório
- `index.html`: interface do Controle FVS com cache IndexedDB/fila offline e ponte para a API Apps Script.
- `config.js`: URL da implantação do Web App (único arquivo que você precisa editar no GitHub).
- `sw.js`: cache da interface para abrir sem internet depois da primeira visita.
- `manifest.json`: configuração de instalação como app.
- `Code.gs`: backend Apps Script com endpoint JSONP. Deve ser instalado na cópia da planilha, junto com o `Index.html` de apoio do Apps Script.

## Instalação
1. Na cópia da planilha, abra **Extensões → Apps Script**.
2. Substitua o conteúdo de `Código.gs` pelo arquivo `Code.gs` deste pacote.
3. No projeto Apps Script, mantenha/crie um arquivo HTML chamado `Index` (pode usar o arquivo `index.html` deste pacote renomeando-o para `Index`, se quiser manter a tela de apoio). Salve.
4. Clique **Implantar → Nova implantação → Aplicativo da Web**. Execute como **você** e limite o acesso à sua conta/usuário autorizado; não publique a planilha nem libere acesso irrestrito. Conclua a autorização e copie a URL terminada em `/exec`.
5. No GitHub, abra `config.js`, clique no lápis e substitua `COLE_A_URL_DO_WEB_APP_AQUI` pela URL `/exec`. Faça **Commit changes**.
6. Ative **Settings → Pages** e publique a branch `main`, pasta `/ (root)`. Se o GitHub não permitir Pages no repositório privado do seu plano, não torne o repositório público contendo informações sensíveis; use um host estático privado compatível.
7. Abra a URL do site publicado com internet, aguarde carregar e clique **Baixar dados offline**. Aguarde terminar antes de ir para a obra.
8. Teste: abra o site uma vez, depois desligue internet e reabra pelo mesmo endereço. No iPhone, use Compartilhar → **Adicionar à Tela de Início** depois da primeira carga.

## Limitações importantes desta versão
- O service worker armazena a interface; IndexedDB armazena as listas de serviços/testes que você baixou e as ações offline suportadas pela fila existente.
- A fila offline deste pacote dá suporte a iniciar/concluir serviço, registrar teste, registrar observação e corrigir observação de teste. Outras operações exigem conexão.
- O botão **Baixar dados offline** baixa as listas de serviços/testes dos 4 x 24 pavimentos. Telas de detalhes, histórico, fotos e algumas consultas de acompanhamento precisam ter sido abertas online para que seus dados sejam guardados; esta versão não deve ser considerada sincronização offline completa de todas as telas.
- Fotos não são enviadas pela ponte JSONP. Envie fotos conectado pela versão original do Apps Script.
- Faça o primeiro teste somente com a cópia da planilha.
