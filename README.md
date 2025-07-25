# Design-Patterns-com-Java-Dos-Cl-ssicos-GoF-ao-Spring-Framework
// Interface Strategy
public interface NotificacaoStrategy {
    void enviar(String mensagem);
}

// Estratégia: Email
public class EmailNotificacao implements NotificacaoStrategy {
    @Override
    public void enviar(String mensagem) {
        System.out.println("Email enviado: " + mensagem);
    }
}

// Estratégia: SMS
public class SMSNotificacao implements NotificacaoStrategy {
    @Override
    public void enviar(String mensagem) {
        System.out.println("SMS enviado: " + mensagem);
    }
}

// Singleton + Contexto de estratégia
public class NotificacaoService {
    private static NotificacaoService instancia;
    private NotificacaoStrategy estrategia;

    private NotificacaoService() {}

    public static NotificacaoService getInstance() {
        if (instancia == null) {
            instancia = new NotificacaoService();
        }
        return instancia;
    }

    public void setEstrategia(NotificacaoStrategy estrategia) {
        this.estrategia = estrategia;
    }

    public void notificar(String mensagem) {
        if (estrategia != null) {
            estrategia.enviar(mensagem);
        } else {
            System.out.println("Estratégia não definida.");
        }
    }
}

// Classe Principal para testar
public class Main {
    public static void main(String[] args) {
        NotificacaoService notificacao = NotificacaoService.getInstance();

        notificacao.setEstrategia(new EmailNotificacao());
        notificacao.notificar("Olá via Email!");

        notificacao.setEstrategia(new SMSNotificacao());
        notificacao.notificar("Mensagem de texto!");
    }
}
