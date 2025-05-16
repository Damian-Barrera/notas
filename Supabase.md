- Para empezar a usar Supabase (con javascript) se debe instalar . Para ello se usa
npm install @supabase/supabase-js . Esta informacion viene de una libreria aojada en github.

-importar el createClient de @supabase/supabase-js
- Luego usar la funcion createClient() Esta funcion recibe dos parametros, La url y la api key. Ambas estan el la parte de confiruacion del proyecto de supabase. Y me devuelve un objeto por lo que hay que guardara en una variable exportable: 
           export const variable = createClient(url,api_key)


