(w=>{
	const d=w.document,m=[...d.images];
	if(m.length){
		const U=w.URL,
		o={headers:new w.Headers({'Origin':w.location.origin}),mode:'cors'},
		f=t=>{
			const g=x=>(l=s.length)>1&&(i=s.lastIndexOf(x))!==-1&&--l!==i;
			let n=null,e=null,l,i,s=t;
			if(g('/')){
				s=s.substring(++i);
				if(g('.')){
					a=s.substring(0,i);
					if(++i!==l){
						s=s.substring(i);
						e=s.substring(0,g('?')?i:l)
					}
				}
			};
			fetch(t,o).then(r=>{
				r.blob().then(b=>{
					if(n===null){n='image_'+b.size};
					if(e===null){e=b.type.substring(6);e=e!=='svg+xml'?e!=='jpeg'?e!=='x-icon'?e:'ico':'jpg':'svg'};
					const a=d.createElement('a');
					a.download=n+'.'+e;
					const u=a.href=U.createObjectURL(b);
					a.click();

					U.revokeObjectURL(u)
				})
			})
		};
		while(m.length){
			const e=m.pop();
			if(e.naturalWidth!==0){// && e.scrollWidth!==0 && e.naturalHeight!==0 && e.scrollHeight!==0
				f(e.src)
			}
		}
	}
})(window);
//========================================================================

