Prof eu havia copiado um resumo de um amigo depois de ver sua mensagem percebi que nem havia lido as "regras no moodle" preferi ler pegar minhas anotações e fazer o meu proprio para nao criar problemas pra ninguem nem mesmo pra mim claro Vou deixar nesse commit as mudancas

Aluno: Lucas Guglielmi pereira	
RA 22.121.013-1

Definição de Sistema Distribuído
Um sistema distribuído é aquele no qual os componentes localizados em computadores interligados em rede se comunicam e coordenam suas ações apenas passando mensagens. Exemplos comuns incluem a Internet, Intranets e Computação Móvel. De acordo com Kindberg e Coulouris (2005), a principal característica dos sistemas distribuídos é a transparência, que esconde a complexidade inerente da distribuição dos componentes.
Middleware
O middleware é uma camada de software que fornece uma abstração de programação, mascarando a heterogeneidade das redes, hardware, sistemas operacionais e linguagens de programação. Ele oferece um modelo computacional uniforme para ser usado pelos programadores de serviços e de aplicativos distribuídos.
Características do Middleware
•	Heterogeneidade: Construído a partir de uma variedade de redes, sistemas operacionais, hardware e linguagens de programação diferentes.
•	Sistemas abertos: Devem ser extensíveis.
•	Segurança: Criptografia é essencial para proteger dados sigilosos, com desafios como ataques de negação de serviço.
•	Escalabilidade: Considerado escalável se o custo de adição de usuários for constante em termos de recursos.
•	Tratamento de falhas: Deve haver tratamento para os erros do sistema.
•	Concorrência: Projetado para manter a consistência nos estados dos dados em um ambiente concorrente.
•	Transparência: Tornar certos aspectos da distribuição invisíveis para o programador de aplicativos.
Exemplos de Middleware
•	CORBA (Common Object Request Broker Architecture): Um padrão definido pela OMG (Object Management Group) que permite que os objetos de um programa sejam usados em outros programas, possivelmente em diferentes máquinas.
•	Java RMI (Remote Method Invocation): Permite que métodos em objetos Java sejam invocados de outras JVMs (Java Virtual Machines), sejam elas locais ou remotas.
•	SOAP (Simple Object Access Protocol): Um protocolo baseado em XML para troca de informações estruturadas na implementação de serviços web.
Arquiteturas de Sistemas Distribuídos
Arquitetura Cliente-Servidor
Um servidor fornece serviços aos clientes. A comunicação é geralmente baseada no protocolo HTTP.
Estrutura HTTP
•	Protocolo: HTTP ou HTTPS.
•	Componentes: Header, Blanckline e Body.
•	Portas: 80 para HTTP e 443 para HTTPS.
Exemplo de Arquitetura Cliente-Servidor
java
Copiar código
import java.io.*; import java.net.*; public class SimpleHTTPServer { public static void main(String[] args) throws IOException { ServerSocket serverSocket = new ServerSocket(8080); while (true) { Socket clientSocket = serverSocket.accept(); PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true); BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream())); String inputLine; while ((inputLine = in.readLine()) != null) { if (inputLine.isEmpty()) break; System.out.println(inputLine); } out.println("HTTP/1.1 200 OK"); out.println("Content-Type: text/plain"); out.println(); out.println("Hello, World!"); out.close(); in.close(); clientSocket.close(); } } } 
Arquitetura Multicamada
Os componentes do sistema são organizados em camadas com diferentes responsabilidades.
Exemplo de Arquitetura Multicamada
•	Camada de Apresentação: Interface com o usuário.
•	Camada de Aplicação: Lógica de negócios.
•	Camada de Dados: Acesso ao banco de dados.
Arquitetura Peer-to-Peer
Todos os computadores no sistema desempenham funções semelhantes.
Exemplo de Arquitetura Peer-to-Peer
•	BitTorrent: este é um protocolo de compartilhamento de arquivos que permite que os usuários compartilhem arquivos diretamente entre si onde um usuário pode enviar ou receber arquivos.
Arquitetura Híbrida
Combinação de diferentes modelos para atender às necessidades específicas da aplicação.
Estruturas Monolíticas vs Microserviços
Estruturas Monolíticas
•	Definição: Construída como uma única unidade indivisível.
•	Vantagens:
•	Simplicidade de Desenvolvimento
•	Desempenho
•	Deploy Simples
•	Desvantagens:
•	Manutenção Complexa
•	Escalabilidade Limitada
•	Implantações Rígidas
Microserviços
•	Definição: Dividida em pequenos serviços independentes.
•	Vantagens:
•	Escalabilidade
•	Desenvolvimento Ágil
•	Resiliência
•	Flexibilidade Tecnológica
•	Desvantagens:
•	Complexidade de Gerenciamento
•	Comunicação entre Serviços
•	Sobrecarga de Rede
Comparação
•	Desempenho: Monolíticos tendem a ter melhor desempenho interno; Microserviços permitem otimizações específicas.
•	Escalabilidade: Microserviços oferecem escalabilidade granular.
•	Manutenção: Microserviços facilitam a manutenção.
•	Ciclo de Desenvolvimento: Microserviços suportam um ciclo de desenvolvimento mais ágil.
MPI (Interface de Passagem de Mensagens)
Facilita a comunicação entre processos em diferentes máquinas em um ambiente de computação paralela.
Tipos de Mensagens
•	Mensagens Bufferizadas: Armazenadas temporariamente até o destinatário estar pronto.
•	Mensagens Não Bloqueantes: Operações ocorrem sem esperar pela conclusão.
•	Mensagens Não Bufferizadas: Envio e recebimento ocorrem diretamente entre os processos.
•	Mensagens Bloqueantes: O processo fica bloqueado até que a operação seja concluída.
Operações Coletivas
•	Scatter: Envia e espalha os dados.
•	Gather: Recolhe dados de vários processos.
•	Reduce: Reduz conjuntos de dados para um dado final.
RMI (Remote Method Invocation)
Protocolo para criar aplicativos distribuídos em Java. Permite que objetos em diferentes máquinas virtuais Java se comuniquem e interajam.
Componentes do RMI
•	Servidor: Executa os objetos remotos.
•	Cliente: Obtém referências a objetos remotos.
•	Registro RMI: Armazena referências a objetos remotos.
•	Stub: Representa um objeto remoto no cliente.
Vantagens do RMI
•	Carregamento Dinâmico de Código
•	Transparência de Rede
•	Flexibilidade
Exemplo de Código RMI em Java
Servidor
java
Copiar código
import java.rmi.RemoteException; import java.rmi.registry.LocateRegistry; import java.rmi.registry.Registry; import java.rmi.server.UnicastRemoteObject; public class Server implements Hello { public Server() {} public String sayHello() { return "Hello, world!"; } public static void main(String args[]) { try { Server obj = new Server(); Hello stub = (Hello) UnicastRemoteObject.exportObject(obj, 0); Registry registry = LocateRegistry.getRegistry(); registry.bind("Hello", stub); System.out.println("Server ready"); } catch (Exception e) { System.err.println("Server exception: " + e.toString()); e.printStackTrace(); } } } 
Cliente
java
Copiar código
import java.rmi.registry.LocateRegistry; import java.rmi.registry.Registry; public class Client { private Client() {} public static void main(String[] args) { try { Registry registry = LocateRegistry.getRegistry(null); Hello stub = (Hello) registry.lookup("Hello"); String response = stub.sayHello(); System.out.println("response: " + response); } catch (Exception e) { System.err.println("Client exception: " + e.toString()); e.printStackTrace(); } } } 
Interface
java
Copiar código
import java.rmi.Remote; import java.rmi.RemoteException; public interface Hello extends Remote { String sayHello() throws RemoteException; } 
Sincronização e Relógios
Relógios Lógicos
Prover a identificação da ordem dos eventos.
Relógios Físicos
Para cenários onde os relógios devem ser apenas iguais e não devem se desviar do tempo real.
Algoritmo de Berkeley
Método de sincronização de relógios em sistemas distribuídos, alinhando os relógios de todos os computadores em uma rede.
Referências Bibliográficas
•	Kindberg, T., & Coulouris, G. (2005). Sistemas Distribuídos: Conceitos e Projeto.
•	Notas de aula da disciplina de Sistemas Distribuídos.

