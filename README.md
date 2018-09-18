# ConfigurationInic

## Conceitos de Configuration

Criei uma aplicação asp .net core para ler um arquivo de configuração settings.ini que esta na raiz do projeto.

Usei o metodo de extensão AddIniFile("arquivo") e exibi os valores do arquivo no navegador.
    
    
        public IConfigurationRoot _config;

        public Startup()
        {
            var builder = new ConfigurationBuilder();
            builder
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddIniFile("Settings.ini");

            _config = builder.Build();
        }
        
         public void Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }

            app.Run(async (context) =>
            {
                foreach (var c in _config.AsEnumerable())
                {
                    await context.Response.WriteAsync($"{c.Key} {c.Value}\n");
                }
            });
        }
