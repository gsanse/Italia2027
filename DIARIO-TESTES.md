# Diário de Bordo — piloto separado
**Não fazer merge na main nem alterar a origem do GitHub Pages antes da aprovação.**
As duas páginas desta branch compartilham diario-bordo.js e diario-bordo.css. O ambiente Supabase foi criado para o diário e os dados não estão no GitHub. O arquivo JS contém somente a chave publicável.
## Prévia local (desktop)
```sh
git clone --branch diario-bordo-dev --single-branch https://github.com/gsanse/Italia2027.git Italia2027-diario
cd Italia2027-diario
python3 -m http.server 8000 --bind 127.0.0.1
```
Abra http://localhost:8000/index.html e http://localhost:8000/operacao-camerota.html usando a mesma origem. A prévia não é o GitHub Pages publicado.
## Antes do login real
No painel Supabase Authentication, confirmar confirmação de e-mail habilitada e permitir exatamente as URLs de retorno da prévia (por exemplo http://localhost:8000/index.html e http://localhost:8000/operacao-camerota.html). Para testes móveis, usar uma prévia HTTPS separada com URLs autorizadas; não alterar o Pages de produção. O SMTP padrão do Supabase envia somente para membros da organização; configurar SMTP próprio para os demais viajantes antes da adoção. Não cadastrar familiares como administradores do projeto.
O RLS do diário autoriza somente e-mails na tabela diary_members; a criação de conta Auth por terceiros não concede acesso. Para impedir também a criação de contas não autorizadas, configurar um hook Before User Created ou desativar cadastro público após provisionar os familiares.
## Critérios de aprovação
- Login real por e-mail, retorno para a prévia, logout, sessão compartilhada entre as duas versões.
- E-mail externo, visitante anônimo e usuário removido não conseguem ler, inserir nem excluir dados ou baixar objetos.
- Publicação de relato, fotos múltiplas, cidade e data; teste em Android/iOS, inclusive formatos suportados.
- Testar outra conta autorizada: ler, mas não excluir publicação ou foto alheia.
- Ampliar, baixar, excluir publicações e imagens, verificar resultado nos dois sites e ausência de objetos órfãos após falhas.
- Verificar visual e acessibilidade, paginação/carga de galeria (piloto atualmente lista até 100 publicações recentes).
- Verificar limites de armazenamento e SMTP antes da viagem; não publicar dados reais durante os testes.
- Só após aprovação, atualizar branch com a main atual, revisar diff e realizar a transição.
## Verificações realizadas
RLS ativo nas tabelas, bucket diary-photos privado (JPEG até 5 MiB), políticas de propriedade para escrita e exclusão, teste SQL transacional com identidades simuladas autorizado/não autorizado/anônimo (rollback), análise de segurança sem alertas, sintaxe JS validada e verificação dos blobs originais da main. Não equivalem a teste real de autenticação e armazenamento via API.
