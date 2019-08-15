# slides

## add slide
```sh
name="new_slide_name"
cp -r template public/${name}
sed -i -e "s/@name@/${name}/g" public/${name}/*
```

## running on local
```sh
cd public
yarn install
yarn dev
```
