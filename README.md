Integrantes do grupo: Catarina Nascimento, Davi Evangelista, Giovana Gouvea, Heloisa Monteiro e Luiz Barbosa.
Professor: Richard Spanhol

FERRAMENTAS
Linguagem: java
Intellij IDEA Community
GitHub
E1_Impressora01.dll - Biblioteca para o controle da impressora
Biblioteca Elgin - fornecida pelo professor Java-Aluno EM
Documentação Elgin

PRÉ-REQUISITOS:
Sistema Operacional
Windows 10/11 (32-bit ou 64-bit)

Software
Java Development Kit (JDK) 11 ou superior
JNA Library 5.0
IDE Java (Eclipse, IntelliJ IDEA, ou similar) - opcional

Arquivos Necessários (Disponíveis na biblioteca)
E1_Impressora01.dll - Biblioteca da impressora fiscal
XMLSAT.xml - Arquivo de exemplo para impressão SAT
CANC_SAT.xml - Arquivo de exemplo para cancelamento

Hardware
Impressora fiscal compatível com a biblioteca E1_Impressora01.dll
Cabo USB ou interface serial para conexão

DESCRIÇÃO
É um sistema de atendimento de caixa (PDV simplificado), que permite o usuário selecionar operações básicas
por meio de um menu interativo. O sistema se comunica com a impressora utilizando as funções disponíveis na biblioteca oficial da Elgin.

GERENCIADOR DE CONEXÃO
Configuração flexível de parâmetros de conexão
Suporte para múltiplos tipos de interface (USB, Serial)
Monitoramento de status da conexão
Abertura e fechamento seguro de conexões

IMPRESSÃO
Texto: Impressão de texto
QR Code: Impressão de códigos QR
Código de Barras: Imprime código de barras
XML SAT: Impressão de documentos SAT
XML Cancelamento: Cancelamento fiscal

CONTROLE DE PERIFÉRICOS
Gaveta Elgin: Abertura automática da gaveta Elgin
Gaveta Padrão
Sinal Sonoro: Alertas sonoros

PASSO A PASSO 
1. Baixe a biblioteca e Documentação fornecidas : 
Biblioteca: https://drive.google.com/file/d/1obPkDgUYDJWebLDJLcu6GJZh8NDRQ_5c/view
Documentação Elgin: https://elgindevelopercommunity.github.io/group___m1.html#ga928f0795631b062f8d5c8c20b9681d8d

2. Coloque no diretório:
Diretório para configurar o DLL: C:/Bibliotecas/E1_Impressora/x64/E1_Impressora01.dll
Importante: Ajuste o caminho no código se necessário

3. CONFIGURAÇÃO
Caminhos dos Arquivos
Importante: Ajuste os seguintes caminhos no código antes da execução:

// Caminho da DLL (linha ~24)
"C:/Bibliotecas/E1_Impressora/x64/E1_Impressora01.dll"

// Caminho do XML SAT (linha ~244)
"C:/Arquivos_XML/XMLSAT.xml"

// Caminho do XML Cancelamento (linha ~262)
"C:/Arquivos_XML/CANC_SAT.xml"

Tipos de Conexão
Tipo	    Código	        Descrição
USB	        1	       Conexão via porta USB

3.1 Parâmetros de Configuração 
Modelo: Nome/modelo da impressora fiscal (Usado: i9)
Porta: Interface de conexão (ex: "USB")
Parâmetro: Configuração adicional (0 para padrão)

4. USO
Configurar Conexão: Configure os parâmetros da impressora
Abrir Conexão: Estabeleça comunicação com a impressora
Usar Funcionalidades: Acesse as opções do menu

Menu de Opções
****************************************************
**************** MENU IMPRESSORA *******************
****************************************************
1  - Configurar Conexao
2  - Abrir Conexao
3  - Impressao Texto
4  - Impressao QRCode
5  - Impressao Cod Barras
6  - Impressao XML SAT
7  - Impressao XML Canc SAT
8  - Abrir Gaveta Elgin
9  - Abrir Gaveta
10 - Sinal Sonoro
0  - Fechar Conexao e Sair

EXEMPLO DE USO
Configurar Conexão:

Opção: 1
Tipo de conexão: 1 (USB)
Modelo: i9
Porta: USB
Parâmetro: 0

ESTRUTURA DO CÓDIGO
Interface ImpressoraDLL

// Interface que representa a DLL, usando JNA
    public interface ImpressoraDLL extends Library {

        // Caminho completo para a DLL
        ImpressoraDLL INSTANCE = (ImpressoraDLL) Native.load(
                "C:\\Users\\giovana_gouvea\\Documents\\Java-Aluno EM\\Java-Aluno EM\\E1_Impressora01.dll",
                ImpressoraDLL.class
        );

        //variaveis pra usar nas funcoes

        int AbreConexaoImpressora(int tipo, String modelo, String conexao, int param);
        int FechaConexaoImpressora();
        int ImpressaoTexto(String dados, int posicao, int estilo, int tamanho);
        int Corte(int avanco);
        int ImpressaoQRCode(String dados, int tamanho, int nivelCorrecao);
        int ImpressaoCodigoBarras(int tipo, String dados, int altura, int largura, int HRI);
        int AvancaPapel(int linhas);
        int StatusImpressora(int param);
        int AbreGavetaElgin();
        int AbreGaveta(int pino, int ti, int tf);
        int SinalSonoro(int qtd, int tempoInicio, int tempoFim);
        int ModoPagina();
        int LimpaBufferModoPagina();
        int ImprimeModoPagina();
        int ModoPadrao();
        int PosicaoImpressaoHorizontal(int posicao);
        int PosicaoImpressaoVertical(int posicao);
        int ImprimeXMLSAT(String dados, int param);
        int ImprimeXMLCancelamentoSAT(String dados, String assQRCode, int param);
}

PRINCIPAIS MÉTODOS
    Método	                    Função
configurarConexao()	  Define parâmetros de conexão
abrirConexao()	      Estabelece comunicação com impressora
fecharConexao()	      Encerra conexão seguramente
imprimirTexto()	      Imprime texto formatado
imprimirQRCode()	    Gera e imprime QR Code
imprimirXMLSAT()	    Processa documentos SAT
