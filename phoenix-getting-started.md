mix phoenix.new server_api --no-brunch

mix deps.get

mix phoenix.gen.json User users username:string hashed_password:string hashed_confirmation_token:string confirmed_at:datetime hashed_password_reset_token:string unconfirmed_email:string authentication_token:string

resources "/users", UserController

mix ecto.create

mix ecto.migrate
