#routes.rb
Rails.application.routes.draw do
  root 'static_pages#home'
  get  '/help',    to: 'static_pages#help'
  get  '/about',   to: 'static_pages#about'
  get  '/contact', to: 'static_pages#contact'
  get  '/signup',  to: 'users#new'
  get    '/login',   to: 'sessions#new'
  post   '/login',   to: 'sessions#create'
  delete '/logout',  to: 'sessions#destroy'
  
  #/users/:id/following
  resources :users do
    member do
      get :following, :followers
    end
  end
  
  resources :users
  resources :account_activations, only: [:edit]
end

#controller 作成/削除
rails g controller コントローラー名s　index create edit
rails d controller コントローラー名s

#モデル作成/削除　マイグレーションファイルも一緒に
rails g model user
rails d model user

#マイグレーションファイル作成
rails g migration AddNameToUsers name:string

rails db:migrate

bin/rails と bundle exec rails の違い
Gemfile どおりの gem を利用できる環境上で rails コマンドが使える。
bin/railsでは、そのRailsアプリケーションのルートディレクトリ直下の bin ディレクトリにある rails というスクリプトを呼び出している。
railsコマンドの場合だけは、railsコマンドを起動した場合に「存在すればbin/railsを実行する」という処理が入るため、bin/railsのあるRailsプロジェクトフォルダ内ではどちらも同じ動作
