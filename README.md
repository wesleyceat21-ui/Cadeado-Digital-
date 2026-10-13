# O Cadeado — PWA inicial

Protótipo responsivo para celular, com visual preto e dourado, números de 01 a 99 e cálculo de R$ 10 por tentativa.

## O que funciona nesta versão
- Interface adaptada para celular.
- Seleção de números.
- Cálculo demonstrativo do valor.
- Manifest e service worker para instalação como PWA quando hospedado em HTTPS.

## O que ainda NÃO funciona
- Não cria cobrança Pix real.
- Não gera QR Code de pagamento.
- Não recebe confirmação automática do Mercado Pago.
- Não persiste compras/tentativas entre dispositivos.
- Não configura nem valida uma combinação secreta no servidor.

Não use para receber dinheiro real até implementar e testar o backend.

## Arquivos
- `index.html`: interface e lógica demonstrativa.
- `manifest.webmanifest`: metadados para instalação.
- `sw.js`: cache básico do PWA.
- `icon.svg`: ícone.

## Publicação
Hospede estes arquivos em um serviço HTTPS. Para instalação PWA, abra o endereço no Chrome do Android e use o menu do navegador > "Instalar app" ou "Adicionar à tela inicial" (a opção pode variar).

## Integração Mercado Pago necessária
A próxima etapa exige um backend HTTPS:
1. O backend cria uma cobrança Pix por pedido com valor calculado no servidor.
2. Guarda o ID do pedido, quantidade de tentativas e ID da cobrança.
3. Recebe webhook do Mercado Pago e valida a notificação conforme a documentação oficial.
4. Consulta o status da cobrança e só então libera as tentativas.
5. Usa operação idempotente para não creditar duas vezes notificações repetidas.
6. Mantém o token privado apenas no servidor, nunca no HTML/JavaScript público.
7. Registra tentativas globalmente para evitar reutilização da mesma combinação.

Antes de cobrar participantes por um jogo com prêmio, confirme o enquadramento jurídico aplicável no Brasil.
