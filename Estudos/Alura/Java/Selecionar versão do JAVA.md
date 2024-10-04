
# Veja as versões disponiveis
Comando

	`update-java-alternatives --list`
	
Resultado

`java-1.11.0-openjdk-amd64      1111       /usr/lib/jvm/java-1.11.0-openjdk-amd64`
`java-1.17.0-openjdk-amd64      1711       /usr/lib/jvm/java-1.17.0-openjdk-amd64`
`java-1.21.0-openjdk-amd64      2111       /usr/lib/jvm/java-1.21.0-openjdk-amd64`

# Em seguida aponte qual você pretende usar

Exemplo java 11:

`sudo update-java-alternatives --set /usr/lib/jvm/java-1.11.0-openjdk-amd64`
