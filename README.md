# bath-link-expander-and-remove-duplicates
bath link expander and remove duplicates

        import requests
    
    def resolve_url(url):
        try:
            r = requests.get(url)
        except requests.exceptions.RequestException:
            return None
        if r.status_code != 200:
            return None
        return r.url
    
    def main():
        input_file = "links_to_exppand.txt"
        output_file = "links_expanded.txt"
    
        # Read links from text file (one link per line)
        with open(input_file, "r") as file:
            urls = [line.strip() for line in file]
    
        # Short URL Ext
        resolved_urls = [resolve_url(url) for url in urls if url]
    
        # Remove duplicates by converting the list to a set
        unique_urls = set(resolved_urls)  # Set will automatically remove duplicates
    
        # Saving to txt file
        with open(output_file, "w") as file:
            for longurl in unique_urls:
                if longurl:  # Ensure we don't write None values to the file
                    file.write(f"{longurl}\n")
    
        print(f"The decoded links were saved in a file {output_file}")
    
    if __name__ == "__main__":
        main()
