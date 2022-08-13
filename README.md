## Acabei desenvolvendo uma biblioteca para facilitar o uso do socket do seu sistema operacional ( WINDOWS/LINUX )

### Linguagem utilizada : C++

#### Estarei deixando logo exemplos de utilizar ela : 

Client : 

    #include "socket.h"

    int main(void)
    {
    
       char teste[] = "127.0.0.1";
       Socket so(teste, 12000, 10, SOCK_STREAM, AF_INET, 0);
       so.registerAddr();
       bool t =  so.socket_();
    
	    if (!t) {
       std::cout << "problema na criacao do socket!" << std::endl;
       return 0;
       }

        bool f = so.connect_();
				
       if (!f) {
            std::cout << "problema na conexao" << std::endl;
            return 0;
        }
				
        char buffer[500] = "teste";
        so.messageSend(buffer, 0);
        return 0;
    }


Servidor : 

    #include "socket.h"

    int main(void)
    {
	char teste[] = "127.0.0.1";
	Socket so(teste, 12000, 10, SOCK_STREAM, AF_INET, 0);

	so.registerAddr();

	int t = so.socket_();
	if (!t) {
		std::cout << "problema na criacao do socket!" << std::endl;
		return 0;
	}

	bool j = so.bind_();
	if (!j) {
		std::cout << "problema na criacao do bind!" << std::endl;
		return 0;
	}

	bool i = so.listen_();
	if (!i) {
		std::cout << "problema no listen" << std::endl;
		return 0;
	}

	char buffer[500];

	while (true) {
		SOCKET c = so.accept_();

		std::cout << "ALGUEM ENTROU NA REDE MENSSAGEM ENVIADA : ";

		so.messageRev(buffer, 0);

		std::cout << buffer << std::endl;
	}
	return 0;
    }
