# make nginx file
sed "s/SITENAME/staging.bejoygeorge.com/g" \
deploy_tools/nginx.template.conf \
| sudo tee /etc/nginx/sites-available/staging.bejoygeorge.com

# enabled site symlink
sudo ln -s ../sites-available/staging.bejoygeorge.com \
/etc/nginx/sites-enabled/staging.bejoygeorge.com

# make systemd file for gunicorn server
sed "s/SITENAME/staging.bejoygeorge.com/g" \
deploy_tools/gunicorn-systemd.template.service \
| sudo tee /etc/systemd/system/gunicorn-staging.bejoygeorge.com.service

# to start systemd service
sudo systemctl daemon-reload
sudo systemctl reload nginx
sudo systemctl enable gunicorn-staging.bejoygeorge.com
sudo systemctl start gunicorn-staging.bejoygeorge.com