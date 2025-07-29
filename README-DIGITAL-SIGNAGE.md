# Sistema de Digital Signage - Sinalização Digital

Sistema completo de sinalização digital para comunicações internas, desenvolvido em Next.js com TypeScript.

## 🚀 Funcionalidades

### Painel Administrativo (`/admin`)
- **Upload de Arquivos**: Envio de imagens (JPG, PNG, GIF, WebP) e vídeos (MP4, WebM, MOV)
- **Registro de TVs**: Cadastro de novas televisões com geração automática de URLs únicas
- **Configuração de Templates**: Definição de nome do template e duração dos slides
- **Gerenciamento**: Visualização e controle de todas as TVs registradas

### Páginas de Exibição (`/display/[tvId]`)
- **Slideshow Automático**: Rotação automática de conteúdo baseada na duração configurada
- **Interface Full-Screen**: Design otimizado para televisões
- **Informações em Tempo Real**: Exibição de data/hora atual
- **Indicadores Visuais**: Barra de progresso e indicadores de slide
- **Auto-Reload**: Atualização automática do conteúdo a cada 5 minutos

## 🛠️ Tecnologias Utilizadas

- **Next.js 15** - Framework React com App Router
- **TypeScript** - Tipagem estática
- **Tailwind CSS** - Estilização moderna
- **Shadcn/ui** - Componentes de interface
- **Armazenamento Local** - Sistema de arquivos + JSON

## 📁 Estrutura do Projeto

```
src/
├── app/
│   ├── admin/page.tsx          # Painel administrativo
│   ├── display/[tvId]/page.tsx # Página de exibição das TVs
│   ├── api/
│   │   ├── upload/route.ts     # API de upload de arquivos
│   │   └── tv/route.ts         # API de gerenciamento de TVs
│   ├── layout.tsx              # Layout principal
│   └── page.tsx                # Página inicial (redireciona para /admin)
├── lib/
│   └── dataStore.ts            # Módulo de persistência de dados
└── components/ui/              # Componentes Shadcn/ui

data/
└── tv.json                     # Banco de dados JSON das TVs

public/
├── uploads/                    # Arquivos enviados pelos usuários
└── demo-images/                # Imagens de demonstração
```

## 🚀 Como Usar

### 1. Iniciar o Sistema
```bash
npm run dev
```
O sistema estará disponível em: `http://localhost:8000`

### 2. Acessar o Painel Administrativo
- Acesse: `http://localhost:8000/admin`
- Use as três abas disponíveis:
  - **Upload de Arquivos**: Para enviar imagens e vídeos
  - **Registrar TV**: Para cadastrar novas televisões
  - **Gerenciar TVs**: Para visualizar TVs cadastradas

### 3. Fazer Upload de Conteúdo
1. Vá para a aba "Upload de Arquivos"
2. Clique em "Selecionar Arquivos"
3. Escolha imagens ou vídeos (máximo 50MB cada)
4. Os arquivos aparecerão na seção "Arquivos Disponíveis"

### 4. Registrar uma Nova TV
1. Vá para a aba "Registrar TV"
2. Preencha os campos:
   - **Nome da TV**: Ex: "TV Recepção", "TV Sala de Reuniões"
   - **Nome do Template**: Ex: "Comunicados Gerais", "Anúncios RH"
   - **Duração do Slide**: Tempo em segundos (1-60)
3. Selecione os arquivos que serão exibidos
4. Clique em "Registrar TV"
5. Uma URL única será gerada: `/display/[id-único]`

### 5. Exibir Conteúdo nas TVs
1. Copie a URL gerada no registro da TV
2. Abra essa URL em um navegador na televisão
3. O conteúdo será exibido em tela cheia com rotação automática

## 📺 Exemplo de Uso

### Cenário: TV da Recepção
1. **Upload**: Envie 3 imagens com comunicados
2. **Registro**: 
   - Nome: "TV Recepção Principal"
   - Template: "Comunicados Gerais"
   - Duração: 8 segundos
3. **URL Gerada**: `/display/abc123def456`
4. **Resultado**: Slideshow automático com rotação a cada 8 segundos

## 🔧 Configurações Técnicas

### Tipos de Arquivo Suportados
- **Imagens**: JPG, PNG, GIF, WebP
- **Vídeos**: MP4, WebM, MOV
- **Tamanho Máximo**: 50MB por arquivo

### Armazenamento
- **Arquivos**: Salvos em `/public/uploads/`
- **Configurações**: Armazenadas em `/data/tv.json`
- **Backup**: Recomenda-se backup regular da pasta `data/` e `public/uploads/`

### Recursos da Página de Exibição
- **Auto-reload**: Conteúdo atualizado a cada 5 minutos
- **Responsivo**: Adapta-se a diferentes tamanhos de tela
- **Indicadores**: Mostra progresso e posição atual do slide
- **Informações**: Data, hora e nome do template sempre visíveis

## 🚀 Deploy em Servidor Debian

### Pré-requisitos
```bash
# Instalar Node.js
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Instalar PM2 para gerenciamento de processos
sudo npm install -g pm2
```

### Deploy
```bash
# 1. Clonar/copiar projeto para o servidor
# 2. Instalar dependências
npm install

# 3. Build da aplicação
npm run build

# 4. Iniciar com PM2
pm2 start npm --name "digital-signage" -- start

# 5. Configurar auto-start
pm2 startup
pm2 save
```

### Configuração de Permissões
```bash
# Garantir permissões para as pastas de dados
chmod 755 data/
chmod 755 public/uploads/
chown -R www-data:www-data data/ public/uploads/
```

## 🔒 Segurança

- Sistema projetado para uso em rede interna
- Validação de tipos de arquivo no upload
- Limite de tamanho de arquivo (50MB)
- Sanitização de nomes de arquivo
- Para uso em produção, considere adicionar autenticação

## 📞 Suporte

Para dúvidas ou problemas:
1. Verifique os logs do console do navegador
2. Verifique os logs do servidor (`pm2 logs digital-signage`)
3. Confirme permissões das pastas `data/` e `public/uploads/`

## 🎯 Próximas Funcionalidades (Roadmap)

- [ ] Autenticação de usuários
- [ ] Agendamento de conteúdo
- [ ] Templates personalizáveis
- [ ] Estatísticas de exibição
- [ ] API REST completa
- [ ] Interface mobile responsiva
- [ ] Suporte a RSS feeds
- [ ] Integração com calendários

---

**Sistema Digital Signage** - Desenvolvido para comunicações internas eficientes e modernas.
