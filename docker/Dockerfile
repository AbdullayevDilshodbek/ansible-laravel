# Use an Ubuntu base image
FROM ubuntu:latest

# Update and install necessary packages, including SSH
RUN apt-get update && apt-get install -y openssh-server && rm -rf /var/lib/apt/lists/*

# Create a directory for the SSH server
RUN mkdir /var/run/sshd

# Add a user for SSH access
RUN useradd -m -s /bin/bash testuser && echo "testuser:test" | chpasswd | usermod -aG sudo testuser

# Allow root login (optional, but not recommended for production)
RUN echo 'PermitRootLogin yes' >> /etc/ssh/sshd_config

# Disable PAM (required for container environments)
RUN sed -i 's/^#UsePAM yes/UsePAM no/' /etc/ssh/sshd_config

# Expose SSH port
EXPOSE 22

# Start SSH service when the container runs
CMD ["/usr/sbin/sshd", "-D"]

