# Dockerfile-flutter. Install flutter with asdf system.
FROM thehprogrammer/sdk-config:latest

# Set label metadata
LABEL description="ASDF system and Flutter installed"
LABEL org.opencontainers.image.source=https://github.com/theHprogrammer/dockernize-the-flutter

USER root

# Create a new user
RUN useradd -ms /bin/bash user
RUN chown -R user:user /opt/android-sdk

# Switch to the new user
USER user
WORKDIR /home/user

# Set environment variables
ENV ASDF_DIR /home/user/.asdf
ENV PATH "$ASDF_DIR/bin:$ASDF_DIR/shims:$PATH"

# Install ASDF
RUN git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.14.0 \
    && echo '. $ASDF_DIR/asdf.sh' >> ~/.bashrc \
    && echo '. $ASDF_DIR/completions/asdf.bash' >> ~/.bashrc \
    # Install Flutter using ASDF
    && . $ASDF_DIR/asdf.sh \
    && asdf plugin add flutter \
    && asdf install flutter 3.19.6-stable \
    && asdf global flutter 3.19.6-stable \
    # Configure android sdk path
    && flutter config --android-sdk $ANDROID_HOME \
    # Run flutter doctor
    && flutter doctor -v

# Expose port 8080 for web applications (optional)
EXPOSE 8080

# Set the default command for the container
CMD ["/bin/bash", "-l"]
