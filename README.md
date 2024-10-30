#include <iostream>
#include <vector>
#include <string>
using namespace std;

// Classe base para o usuário
class Usuario {
private:
    string nome;
    int pontuacao;
    int fase;
public:
    Usuario(string nome) : nome(nome), pontuacao(0), fase(1) {}

    void incrementarPontuacao(int pontos) {
        pontuacao += pontos;
    }

    void avancarFase() {
        fase++;
        cout << nome << " avançou para a fase " << fase << "!" << endl;
    }

    void mostrarPerfil() const {
        cout << "Perfil de " << nome << endl;
        cout << "Pontuação: " << pontuacao << endl;
        cout << "Fase atual: " << fase << endl;
    }
};

// Classe para sistema de fases
class Fase {
public:
    int numero;
    string descricao;

    Fase(int num, string desc) : numero(num), descricao(desc) {}

    void mostrarFase() const {
        cout << "Fase " << numero << ": " << descricao << endl;
    }
};

// Classe para conteúdo (acervo, blogs, programas online, etc.)
class Conteudo {
public:
    string titulo;
    string tipo;

    Conteudo(string titulo, string tipo) : titulo(titulo), tipo(tipo) {}

    void mostrarConteudo() const {
        cout << "Conteúdo: " << titulo << " (" << tipo << ")" << endl;
    }
};

// Classe para o sistema de ranking
class Ranking {
public:
    vector<Usuario> usuarios;

    void adicionarUsuario(const Usuario& usuario) {
        usuarios.push_back(usuario);
    }

    void mostrarRanking() const {
        cout << "Ranking dos Usuários:" << endl;
        for (const auto& u : usuarios) {
            u.mostrarPerfil();
        }
    }
};

// Classe para agendamentos
class Agendamento {
public:
    string data;
    string descricao;

    Agendamento(string data, string descricao) : data(data), descricao(descricao) {}

    void mostrarAgendamento() const {
        cout << "Agendamento em " << data << ": " << descricao << endl;
    }
};

// Classe principal para o site
class Macacoteca {
public:
    vector<Fase> fases;
    vector<Conteudo> conteudos;
    Ranking ranking;
    vector<Agendamento> agendamentos;

    // Adiciona novas fases
    void adicionarFase(const Fase& fase) {
        fases.push_back(fase);
    }

    // Adiciona novo conteúdo
    void adicionarConteudo(const Conteudo& conteudo) {
        conteudos.push_back(conteudo);
    }

    // Adiciona novo agendamento
    void adicionarAgendamento(const Agendamento& agendamento) {
        agendamentos.push_back(agendamento);
    }

    // Exibe todas as fases
    void mostrarFases() const {
        cout << "Fases disponíveis:" << endl;
        for (const auto& f : fases) {
            f.mostrarFase();
        }
    }

    // Exibe todos os conteúdos
    void mostrarConteudos() const {
        cout << "Conteúdos disponíveis:" << endl;
        for (const auto& c : conteudos) {
            c.mostrarConteudo();
        }
    }

    // Exibe todos os agendamentos
    void mostrarAgendamentos() const {
        cout << "Agendamentos futuros:" << endl;
        for (const auto& a : agendamentos) {
            a.mostrarAgendamento();
        }
    }
};

// Função principal
int main() {
    Macacoteca site;

    // Criando usuários
    Usuario usuario1("Alice");
    Usuario usuario2("Bob");

    // Adicionando usuários ao ranking
    site.ranking.adicionarUsuario(usuario1);
    site.ranking.adicionarUsuario(usuario2);

    // Criando fases e adicionando ao site
    site.adicionarFase(Fase(1, "Introdução ao mundo dos macacos"));
    site.adicionarFase(Fase(2, "Conhecimento sobre espécies"));

    // Criando conteúdos e adicionando ao site
    site.adicionarConteudo(Conteudo("Blog sobre ecossistemas", "Blog"));
    site.adicionarConteudo(Conteudo("Programa de Conservação", "Programa Online"));

    // Criando agendamentos
    site.adicionarAgendamento(Agendamento("10/11/2024", "Encontro de Ecologia"));
    site.adicionarAgendamento(Agendamento("15/12/2024", "Aula sobre Biomas"));

    // Simulação de interação com o site
    site.mostrarFases();
    site.mostrarConteudos();
    site.mostrarAgendamentos();
    site.ranking.mostrarRanking();

    // Usuário realiza atividades e avança de fase
    usuario1.incrementarPontuacao(100);
    usuario1.avancarFase();

    // Mostra perfil atualizado do usuário
    usuario1.mostrarPerfil();

    return 0;
}
