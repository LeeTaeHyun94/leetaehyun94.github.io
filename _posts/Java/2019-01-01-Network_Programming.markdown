---
layout: post
title:  "Network Programming"
description: "Network Programming in Java"
date:   2019-01-03 21:30:00
categories: Java
comments: true
---
- 네트워크를 통해서 데이터를 주고 받는 프로그래밍
- Server & Client
    - 서버 : 사용자들에게 서비스를 제공하는 컴퓨터
    - 클라이언트 : 서버에게 서비스를 요청해서 사용하는 컴퓨터
- IP Address : 인터넷에서 사용하는 컴퓨터의 주소
- Port : 가상의 통신 선로
- ![Port Number Example](./../../assets/Java/11.PNG)
- Host Name, DNS, URL
    - DNS (Domain Name System) : 숫자 대신 기호를 사용하는 주소
    - DNS 서버 : 기호 주소를 숫자 주소로 변환해주는 서버
    - URL (Uniform Resource Locator) : 인터넷 상의 자원을 나타내는 약속
    - ![Internet DNS Server Example](./../../assets/Java/12.PNG)
- Protocol
    - 통신을 하기 위한 약속, 컴퓨터 사이의 약속(프로토콜)을 자세히 정하고, 이를 지킴으로써 통신이 성립된다.
    - 프로토콜을 통해 무엇을 어떻게 언제 통신할 것인가를 규정
    - ![Protocol](./../../assets/Java/13.PNG)
    - TCP (Transmission Control Protocol) : 신뢰성있게 통신하기 위하여 먼저 서로 간의 연결을 설정한 후에 데이터를 보내고 받는 방식
        - ![TCP](./../../assets/Java/14.PNG)
        - 연결지향형 소켓의 데이터 전송 특성
            - 중간에 데이터가 소멸되지 않는다.
            - 전송 순서대로 데이터가 수신된다.
            - 데이터의 경계가 존재하지 않는다.
            - Socket : Socket의 연결은 반드시 1 : 1의 구조
        - Socket : TCP를 사용하여 응용 프로그램끼리 통신을 하기 위한 End Point
        - ![Socket](./../../assets/Java/16.PNG)
        - ServerSocket : 서버를 위한 소켓
        - Socket : 클라이언트를 위한 소켓
        ```Java
        import java.io.FileInputStream;
        import java.io.InputStream;
        import java.io.OutputStream;
        import java.net.ServerSocket;
        import java.net.Socket;
        
        public class ServerEx1 {
            public static void main(String[] args) throws Exception {
                ServerSocket server = new ServerSocket(5555);
                System.out.println("read...........!");
                Socket clientSocket = server.accept();
                OutputStream out = clientSocket.getOutputStream();
                InputStream fin = new FileInputStream("C:\\java\\sung.jpg");
                while (true) {
                    int data = fin.read();
                    out.write(data);
                    if (data == -1) break;
                }
                fin.close();
                out.close();
                clientSocket.close();
                server.close();
            }
        }
        
        import java.io.FileOutputStream;
        import java.io.InputStream;
        import java.io.OutputStream;
        import java.net.Socket;
        
        public class ClientEx {
            public static void main(String[] args) throws Exception {
                Socket socket = new Socket("127.0.0.1", 5555);
                System.out.println("연결되었음 : " + socket);
                InputStream in = socket.getInputStream();
                OutputStream fout = new FileOutputStream("C:\\java\\get.jpg");
                while (true) {
                    int data = in.read();
                    if (data == -1) break;
                    fout.write(data);
                }
                fout.close();
                in.close();
                socket.close();
            }
        }
        ```
        
    - UDP (User Datagram Protocol) : 데이터를 일정 개수, 고정 길이를 가진 패킷으로 분할하여 전송한다.
        - ![UDP](./../../assets/Java/15.PNg)
        - 비연결지향형 소켓의 데이터 전송 특성
            - 전송 순서 상관없이 빠른 속도의 전송을 지향
            - 데이터 손실의 우려가 있다.
            - 데이터의 경계가 존재한다.
            - 한 번에 전송할 수 있는 데이터의 크기가 제한된다.
        - DatagramSocket : UDP 프로토콜을 사용하는 소켓을 생성
        - DatagramPacket : UDP 패킷 생성
        - MulticastSocket
        ```java
        import javax.swing.*;
        import java.awt.*;
        import java.awt.event.ActionEvent;
        import java.awt.event.ActionListener;
        import java.io.IOException;
        import java.net.DatagramPacket;
        import java.net.DatagramSocket;
        import java.net.InetAddress;
        
        public class MessengerA {
            protected JTextField textField;
            protected JTextArea textArea;
            DatagramSocket socket;
            DatagramPacket packet;
            InetAddress address = null;
            final int myPort = 5000;
            final int otherPort = 6000;
        
            public MessengerA() throws IOException {
                MyFrame f = new MyFrame();
                address = InetAddress.getByName("127.0.0.1");
                socket = new DatagramSocket(myPort);
            }
        
            public void process() {
                while (true) {
                    try {
                        byte[] buf = new byte[256];
                        packet = new DatagramPacket(buf, buf.length);
                        socket.receive(packet);
                        textArea.append("RECEIVED : " + new String(buf) + "\n");
                    }
                    catch (IOException e) {
                        e.printStackTrace();
                    }
                }
            }
        
            class MyFrame extends JFrame implements ActionListener {
                public MyFrame() {
                    super("MessengerA");
                    setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
                    textField = new JTextField(30);
                    textField.addActionListener(this);
                    textArea = new JTextArea(10, 30);
                    textArea.setEditable(false);
                    add(textField, BorderLayout.PAGE_END);
                    add(textArea, BorderLayout.CENTER);
                    pack();
                    setVisible(true);
                }
        
                @Override
                public void actionPerformed(ActionEvent e) {
                    String s = textField.getText();
                    byte[] buffer = s.getBytes();
                    DatagramPacket packet = new DatagramPacket(buffer, buffer.length, address, otherPort);
                    try {
                        socket.send(packet);
                    }
                    catch (IOException ioe) {
                        ioe.printStackTrace();
                    }
                    textArea.append("SENT: " + s + "\n");
                    textField.selectAll();
                    textArea.setCaretPosition(textArea.getDocument().getLength());
                }
            }
        
            public static void main(String[] args) throws IOException {
                MessengerA m = new MessengerA();
                m.process();
            }
        }
        
        import javax.swing.*;
        import java.awt.*;
        import java.awt.event.ActionEvent;
        import java.awt.event.ActionListener;
        import java.io.IOException;
        import java.net.DatagramPacket;
        import java.net.DatagramSocket;
        import java.net.InetAddress;
        
        public class MessengerB {
            protected JTextField textField;
            protected JTextArea textArea;
            DatagramSocket socket;
            DatagramPacket packet;
            InetAddress address = null;
            final int myPort = 6000;
            final int otherPort = 5000;
        
            public MessengerB() throws IOException {
                MyFrame f = new MyFrame();
                address = InetAddress.getByName("127.0.0.1");
                socket = new DatagramSocket(myPort);
            }
        
            public void process() {
                while (true) {
                    try {
                        byte[] buf = new byte[256];
                        packet = new DatagramPacket(buf, buf.length);
                        socket.receive(packet);
                        textArea.append("RECEIVED : " + new String(buf) + "\n");
                    }
                    catch (IOException e) {
                        e.printStackTrace();
                    }
                }
            }
        
            class MyFrame extends JFrame implements ActionListener {
                public MyFrame() {
                    super("MessengerB");
                    setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
                    textField = new JTextField(30);
                    textField.addActionListener(this);
                    textArea = new JTextArea(10, 30);
                    textArea.setEditable(false);
                    add(textField, BorderLayout.PAGE_END);
                    add(textArea, BorderLayout.CENTER);
                    pack();
                    setVisible(true);
                }
        
                @Override
                public void actionPerformed(ActionEvent e) {
                    String s = textField.getText();
                    byte[] buffer = s.getBytes();
                    DatagramPacket packet = new DatagramPacket(buffer, buffer.length, address, otherPort);
                    try {
                        socket.send(packet);
                    }
                    catch (IOException ioe) {
                        ioe.printStackTrace();
                    }
                    textArea.append("SENT: " + s + "\n");
                    textField.selectAll();
                    textArea.setCaretPosition(textArea.getDocument().getLength());
                }
            }
        
            public static void main(String[] args) throws IOException {
                MessengerB m = new MessengerB();
                m.process();
            }
        }
        ```